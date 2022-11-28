# sideloading ansible on wsl
I am attempting to achieve a set up that will allow me to simulate the management of one or more servers with ansible, all on wsl

## why on earth am I doing this?
I wanted to learn ansible, and since I'm not made of money, I don't have access to servers to play around with.  
Then when I was trying to use JetBrains CLion IDE with Alpine or Ubuntu, I was running into all sorts of environment configuration overhead.  

So, then I thought that using ansible might be a way I could easily set a WSL instance up to deal with this.  
I searched around looking for a way of doing this, but most results involving wsl and ansible together involved instructions on how to install it there.  
Maybe I was looking in the wrong places, or didn't know what to search, but I really couldn't find it.

As a caveat, it may be possible to simply host containers within an existing linux distro and then connect ansible to them.  
But this breaks the container best practice of not modifying the container during runtime, and seems like more trouble than it's worth.  
Like at that point, why not just use a container image alone? And I want to learn ansible.

## why sideload a custom wsl distro?

One of the things I realized is that I wanted these instances to be "per-project" right?  
Because at this point I'm aiming for something like a Docker's Dev Environments or a python venv, but:  
* a less closed system than docker's solution
* a more generic and extensible solution than python venv 

If I wanted that, then every time I booted up the project it would overwrite the entirety of the existing wsl instance.  
That means I should want a separate instance for each project, or at least a couple instances so I can use them with multiple projects at the same time.  

## process start

I'm starting with an article from Microsoft about building custom distros here:  
https://learn.microsoft.com/en-us/windows/wsl/build-custom-distro

As recommended in the article, I'll be working from their repo:  
https://github.com/Microsoft/WSL-DistroLauncher (latest commit [32f88e8](https://github.com/microsoft/WSL-DistroLauncher/commit/32f88e8426d31dc6bf06c6711ec7a85edefe554f) as of writing this)

I don't know C/C++ _very_ well, but they're not unknown to me and I'm more than happy to learn.  
I'll also see about using Rust if possible since I enjoy it, but more than likely it will introduce too much complexity.

### first impressions

the above example repo requires Visual Studio, I was using Clion.  
Currently looking into whether I'll be able to use Clion with some plugins or if VS Code is an option.

I'd rather not have to deal with Visual Studio.

But it is a good reminder that it would be good to build this with use in generalized IDEs in mind.

### example repo's instructions seem to be incredibly outdated

This is step one:

> 1. Generate a test certificate:
> 
>     1. In Visual Studio, open DistroLauncher-Appx/MyDistro.appxmanifest
>     1. Select the Packaging tab
>     1. Select "Choose Certificate"
>     1. Click the Configure Certificate drop down and select Create test certificate.

Looks like it hasn't changed in 5 years, based on the git history.  
There's no "Packaging tab" in the version of Visual Studio that I'm using (Community 2017 15.9.51) that I can see.  

I've searched in the 'quick search' and found NuGet package manager, but it seems like it's for getting packages?  
In any case, it doesn't match any of the UI screenshots I see around the web when I search for these things, and has no 'Configure Certificate' option. 

In case it is not extremely apparent, I do not know hardly anything about .NET development.  
So, now I have been madly searching everywhere for whatever the hell a "Test Certificate" is.

I've found out that my version of Visual Studio is not up to date, so I'm upgrading to Visual Studio 2022.  
Who knows if that will help since it's probably Visual Studio 2015 that I need to follow this 5 year old documentation.  

### Visual Studio 2022

I have no idea how to use this IDE. I installed VS Vim, (thank god that exists).  
Made several attempts at converting the project to be compatible and I think they worked to some extent?

I skipped step 1 entirely, as I have no idea what to look for there.  
The first issue I had was the MSBuild path in `build.bat`. So I updated that:

```bat
if exist "%ProgramFiles%\Microsoft Visual Studio\2022\Community\MSBuild\Current\Bin\MSBuild.exe" (
    set MSBUILD="%ProgramFiles%\Microsoft Visual Studio\2022\Community\MSBuild\Current\Bin\MSBuild.exe"
    goto :FOUND_MSBUILD
)
```

But when I ran the script it still failed to build (re-formated and PII sanitized):  [output](./readme_overflow/build_script_output/Xaml.Cpp.targets_notfound.md)
    
As you can see there's some issue with the `Microsoft.Windows.UI.Xaml.Cpp.targets` file. So I removed this line from `DistroLauncher-Appx\DistroLauncher-Appx.vcxproj` (In retrospect, I am not sure why I thought this would work):  

```xml
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.targets" />
```

Then `build.bat` failed for a different reason! yay: [output](./readme_overflow/build_script_output/target_build_DNE.md)

So, I tried building using VS's builtins from the solution explorer (right click each 'project' and click 'Build').  
This worked for the `launcher` project, but not for the `DistroLauncher-Appx` project, I got similar errors.

Result of it with that line I deleted [here](./readme_overflow/vs_native_build_output/base_output_path_not_set.md), deleting it results only in a change to the last line as seen [here](./readme_overflow/vs_native_build_output/target_build_dne_x2.md).


So, I'm going to assume that the first error from `build.bat` is legitimate, as I did not actually delete the file that was having the import issue.
After a quick search around I found that installing the Universal Windows App development feature of VS might fix it, so I'm doing that now.

Okay, I installed that thing, and now got some completely different errors!!  
Would you look at that.

I got a warning in the VS ui (in the Solution Explorer, .sln view) that I needed to install some missing components. 
So, I clicked the 'Install' link and nothing happened.
But then I remember that it's windows, so I closed the VS Installer (that I still had open) and then clicked the link, and it started installing this:

    C++ (v143) Universal Windows Platform tools

Once complete, I ran `build.bat` again and saw this [output](./readme_overflow/build_script_output/platform_install.tar.gz_notfound.md).


### the `install` tarball

The build project xml is referencing `install.tar.gz` in a platform specific directory, however the instructions only mention putting that install tarball into the main directory (step 7):

> Copy your tar.gz containing your distro into the root of the project and rename it to install.tar.gz.

The README for that project also mentions this (Step 2):

> Edit your distribution-specific information in DistributionInfo.h and DistributionInfo.cpp. NOTE: The DistributionInfo::Name variable must uniquely identify your distribution and cannot change from one version of your app to the next.
>>Note: The examples for creating a user account and querying the UID are from an Ubuntu-based system, and may need to be modified to work appropriately on your distribution.

So I initially, I looked for a Ubuntu image, but I only ever found .iso images. 
Instead I'm trying with an Alpine tarball image from [here](https://alpinelinux.org/downloads/). 

Obviously this will cause issues down the road for this POC, but I'll just have to adjust the `DistributionInfo.cpp` configuration to match. 
Ideally we'll be automated this part of the process as well, so it'll be a good excercise.

I did actually follow this part of the instructions, and had the Alpine image in the root directory. This did not satisfy the reference to `..\ARM64\install.tar.gz` nor to `..\x64\install.tar.gz` that the project was expecting.

So, I added this to the `build.bat` script:

```bat
:FOUND_MSBUILD
set _MSBUILD_TARGET=Build
set _MSBUILD_CONFIG=Debug
# added because we'll be referencing the platform twice
set _MSBUILD_PLATFORM=x64

:ARGS_LOOP
if (%1) == () goto :POST_ARGS_LOOP
if (%1) == (clean) (
    set _MSBUILD_TARGET=Clean,Build
)
if (%1) == (rel) (
    set _MSBUILD_CONFIG=Release
)

# added these, figured since we already have a variable, we might as well
if (%1) == (arm64) (
    set _MSBUILD_PLATFORM=ARM64
)
if (%1) == (x64) (
    set _MSBUILD_PLATFORM=x64
)
shift
goto :ARGS_LOOP

:POST_ARGS_LOOP
# need to make sure directory exists before copying the tarball
if not exist %~dp0\%_MSBUILD_PLATFORM% (
    MKDIR %~dp0\%_MSBUILD_PLATFORM%
)
# copy the install tarball into the appropriate platform directory
# overwrites b/c changes to the tarball should affect the build
COPY %~dp0\install.tar.gz %~dp0\%_MSBUILD_PLATFORM%\install.tar.gz

# add the platform variable here
%MSBUILD% %~dp0\DistroLauncher.sln /t:%_MSBUILD_TARGET% /m /nr:true /p:Configuration=%_MSBUILD_CONFIG%;Platform=%_MSBUILD_PLATFORM%   
```

I executed the `build.bat` script again and that skipping the certificate step finally [caught up with me](./readme_overflow/build_script_output/missing_certificate.md)

### finally, to deal with the certificate

After all of the previous I finally have to figure out how to generate a test certificate, and why that's important.

Will I have to generate one everytime I want to boot up one of these things?