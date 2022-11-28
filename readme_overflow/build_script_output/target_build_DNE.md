I got this after deleting this import from `DistroLauncher-Appx\DistroLauncher-Appx.vcxproj`:  

    <Import Project="$(VCTargetsPath)\Microsoft.Cpp.targets" />

error output:

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