Got this error when running `build.bat` after attempting migration to VS 2022, but without the Universal Windows Application development feature (or whatever that's called)

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