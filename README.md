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

    if exist "%ProgramFiles%\Microsoft Visual Studio\2022\Community\MSBuild\Current\Bin\MSBuild.exe" (
        set MSBUILD="%ProgramFiles%\Microsoft Visual Studio\2022\Community\MSBuild\Current\Bin\MSBuild.exe"
        goto :FOUND_MSBUILD
    )

But when I ran the script it still failed to build (re-formated and PII sanitized):  

     "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher.sln" (Build target) (1) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher\DistroLauncher.vcxproj" (default target) (3) ->
       (CustomBuild target) ->
         C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VC\v170\Microsoft.CppCommon.targets(247,5): 
         warning MSB8065: Custom build for item "messages.mc" succeeded, but specified output 
         "$HOME\source\repos\wsl-distrolauncher\distrolauncher\msg0409.bin" has not been created.
         This may cause incremental build to work incorrectly. 
         [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher\DistroLauncher.vcxproj]


       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher.sln" (Build target) (1) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj.metaproj" (default target) (2) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj" (default target) (4) ->
         C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VC\v170\Microsoft.CppCommon.targets(2645,3): 
         error MSB4019: The imported project 
           "C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\WindowsXaml\v17.0\Microsoft.Windows.UI.Xaml.Cpp.targets" was not found. 
           Confirm that the expression in the Import declaration 
           "C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\WindowsXaml\v17.0\Microsoft.Windows.UI.Xaml.Cpp.targets" is correct, 
           and that the file exists on disk. [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj]

    1 Warning(s)
    1 Error(s)
    
As you can see there's some issue with the `Microsoft.Windows.UI.Xaml.Cpp.targets` file. So I removed this line from `DistroLauncher-Appx\DistroLauncher-Appx.vcxproj`:  

    <Import Project="$(VCTargetsPath)\Microsoft.Cpp.targets" />

Then `build.bat` failed for a different reason! yay:

    "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher.sln" (Build target) (1) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher\DistroLauncher.vcxproj" (default target) (3) ->
       (CustomBuild target) ->
         C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VC\v170\Microsoft.CppCommon.targets(247,5): 
           warning MSB8065: Custom build for item "messages.mc" succeeded, but specified output 
           "$HOME\source\repos\wsl-distrolauncher\distrolauncher\msg0409.bin" has not been created. 
           This may cause incremental build to work incorrectly. 
           [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher\DistroLauncher.vcxproj]


       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher.sln" (Build target) (1) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj.metaproj" (default target) (2) ->
       "$HOMR\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj" (default target) (4) ->
         $HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj : 
           error MSB4057: The target "Build" does not exist in the project.

    1 Warning(s)
    1 Error(s)

So, I tried building using VS's builtins from the solution explorer (right click each 'project' and click 'Build').  
This worked for the `launcher` project, but not for the `DistroLauncher-Appx` project, I got similar errors.

Result of it with that line I deleted:
   
| Severity | Code | Description | Project | File | Line |
| ---      | ---  | ---         | ---     | ---  | ---  |
| Error | MSB4057 | The target "Build" does not exist in the project. | $HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj | $HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj | 1 |
| Warning | MSB8065 | Custom build for item "messages.mc" succeeded, but specified output "$HOME\source\repos\wsl-distrolauncher\distrolauncher\msg0409.bin" has not been created. This may cause incremental build to work incorrectly. | launcher | C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VC\v170\Microsoft.CppCommon.targets | 247 |
| Warning | LNK4075 | ignoring '/INCREMENTAL' due to '/LTCG' specification | launcher | $HOME\source\repos\WSL-DistroLauncher\DistroLauncher\LINK | 1 |
| Error |  | The BaseOutputPath/OutputPath property is not set for project 'DistroLauncher-Appx.vcxproj'.  Please check to make sure that you have specified a valid combination of Configuration and Platform for this project.  Configuration='Release'  Platform='x64'.  This error may also appear if some other project is trying to follow a project-to-project reference to this project, this project has been unloaded or is not included in the solution, and the referencing project does not build using the same or an equivalent Configuration or Platform. | DistroLauncher-Appx | C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Current\Bin\amd64\Microsoft.Common.CurrentVersion.targets | 832 |

Deleting it results in the last line changing to this:

| Severity | Code | Description | Project | File | Line |
| ---      | ---  | ---         | ---     | ---  | ---  |
| Error | MSB4057 | The target "Build" does not exist in the project. | DistroLauncher-Appx | $HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj | 1 |

So, I'm going to assume that the first error from `build.bat` is legitimate, as I did not actually delete the file that was having the import issue.
After a quick search around I found that installing the Universal Windows App development feature of VS might fix it, so I'm doing that now.
