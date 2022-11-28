I generated a certificate and updated the thumbprint in the vcxprof file. Got these errors when I ran the `build.bat` script:  

	"$HOME\source\repos\WSL-DistroLauncher\DistroLauncher.sln" (Build target) (1) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher\DistroLauncher.vcxproj" (default target) (3) ->
       (CustomBuild target) ->
         C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VC\v170\Microsoft.CppCommon.targets(247,5): warning MSB8065: Custom build for item "messages.mc" succeeded, but specified output "$HOME\source\repos\wsl-distrolauncher\distrolauncher\msg0409.bin" has not been created. This may cause incremental build to work incorrectly. [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher\Di
       stroLauncher.vcxproj]


       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher.sln" (Build target) (1) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj.metaproj" (default target) (2) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj" (default target) (4) ->
         C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VC\v170\Microsoft.CppCommon.targets(247,5): warning MSB8064: Custom build for item "mydistro" succeeded, but specified dependency "$HOME\source\repos\wsl-distrolauncher\distrolauncher-appx\mydistro" does not exist. This may cause incremental build to work incorrectly. [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\
       DistroLauncher-Appx.vcxproj]
         C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VC\v170\Microsoft.CppCommon.targets(247,5): warning MSB8065: Custom build for item "mydistro" succeeded, but specified output "$HOME\source\repos\wsl-distrolauncher\distrolauncher-appx\mydistro.exe" has not been created. This may cause incremental build to work incorrectly. [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher
       -Appx\DistroLauncher-Appx.vcxproj]


       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher.sln" (Build target) (1) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj.metaproj" (default target) (2) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj" (default target) (4) ->
       (_ValidateAppxManifest target) ->
         MyDistro.appxmanifest(14,6): warning APPX0006: This project uses the 'runFullTrust' capability. You should use the Windows Application Packaging Project to produce the store and sideload packages. See https://go.microsoft.com/fwlink/?linkid=871803 for more information. [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj]


       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher.sln" (Build target) (1) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj.metaproj" (default target) (2) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj" (default target) (4) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher.sln" (Build target) (1:3) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher\DistroLauncher.vcxproj" (default target) (3:7) ->
       (CustomBuild target) ->
         C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VC\v170\Microsoft.CppCommon.targets(247,5): warning MSB8065: Custom build for item "messages.mc" succeeded, but specified output "$HOME\source\repos\wsl-distrolauncher\distrolauncher\msg0409.bin" has not been created. This may cause incremental build to work incorrectly. [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher\Di
       stroLauncher.vcxproj]


       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher.sln" (Build target) (1) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj.metaproj" (default target) (2) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj" (default target) (4) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher.sln" (Build target) (1:3) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj.metaproj" (default target) (2:2) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj" (default target) (4:2) ->
         C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VC\v170\Microsoft.CppCommon.targets(247,5): warning MSB8064: Custom build for item "mydistro" succeeded, but specified dependency "$HOME\source\repos\wsl-distrolauncher\distrolauncher-appx\mydistro" does not exist. This may cause incremental build to work incorrectly. [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj]
         C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VC\v170\Microsoft.CppCommon.targets(247,5): warning MSB8065: Custom build for item "mydistro" succeeded, but specified output "$HOME\source\repos\wsl-distrolauncher\distrolauncher-appx\mydistro.exe" has not been created. This may cause incremental build to work incorrectly. [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj]


       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher.sln" (Build target) (1) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj.metaproj" (default target) (2) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj" (default target) (4) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher.sln" (Build target) (1:3) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj.metaproj" (default target) (2:2) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj" (default target) (4:2) ->
       (_ValidateAppxManifest target) ->
         MyDistro.appxmanifest(14,6): warning APPX0006: This project uses the 'runFullTrust' capability. You should use the Windows Application Packaging Project to produce the store and sideload packages. See https://go.microsoft.com/fwlink/?linkid=871803 for more information. [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj]


       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher.sln" (Build target) (1) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj.metaproj" (default target) (2) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj" (default target) (4) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher.sln" (Build target) (1:3) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj.metaproj" (default target) (2:2) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj" (default target) (4:2) ->
       (_GenerateAppxPackageRecipeFile target) ->
         C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VisualStudio\v17.0\AppxPackage\Microsoft.AppXPackage.Targets(3011,5): error APPX0702: Payload file '$HOME\source\repos\WSL-DistroLauncher\x64\Debug\DistroLauncher-Appx\arm64\DistroLauncher-Appx\mydistro.exe' does not exist. [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj]
         C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VisualStudio\v17.0\AppxPackage\Microsoft.AppXPackage.Targets(3011,5): error APPX0702: Payload file '$HOME\source\repos\WSL-DistroLauncher\ARM64\install.tar.gz' does not exist. [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj]

    8 Warning(s)
    2 Error(s)
