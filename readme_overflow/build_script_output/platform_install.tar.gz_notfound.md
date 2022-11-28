This was the error the output once I finally got VS set up for the project with all the correct components. Mostly warnings: 

    "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher.sln" (Build target) (1) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher\DistroLauncher.vcxproj" (default target) (3) ->
       (CustomBuild target) ->
         C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VC\v170\Microsoft.CppCommon.targets(247,5): warning MSB8065: Custom build for item "messages.mc" succeeded, but specified output "$HOME\source\repos\wsl-distrolauncher\distrolauncher\msg0409.bin" has not been created. This may cause incremental build to work incorrectly. [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher\DistroLauncher.vcxproj]


       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher.sln" (Build target) (1) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj.metaproj" (default target) (2) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj" (default target) (4) ->
         C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VC\v170\Microsoft.CppCommon.targets(247,5): warning MSB8064: Custom build for item "mydistro" succeeded, but specified dependency "$HOME\source\repos\wsl-distrolauncher\distrolauncher-appx\mydistro" does not exist. This may cause incremental build to work incorrectly. [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj]
         C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VC\v170\Microsoft.CppCommon.targets(247,5): warning MSB8065: Custom build for item "mydistro" succeeded, but specified output "$HOME\source\repos\wsl-distrolauncher\distrolauncher-appx\mydistro.exe" has not been created. This may cause incremental build to work incorrectly. [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj]


       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher.sln" (Build target) (1) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj.metaproj" (default target) (2) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj" (default target) (4) ->
       (_ValidateSigningCertificate target) ->
         C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VisualStudio\v17.0\AppxPackage\Microsoft.AppXPackage.Targets(854,5): warning : Certificate file does not exist: DistroLauncher-Appx_TemporaryKey.pfx [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj]


       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher.sln" (Build target) (1) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj.metaproj" (default target) (2) ->
       "$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj" (default target) (4) ->
       (_GenerateCurrentProjectAppxManifest target) ->
         C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VisualStudio\v17.0\AppxPackage\Microsoft.AppXPackage.Targets(2740,5): warning APPX0104: Certificate file 'DistroLauncher-Appx_Temporary
       Key.pfx' not found. [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj]
         C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VisualStudio\v17.0\AppxPackage\Microsoft.AppXPackage.Targets(2740,5): warning APPX0102: A certificate with thumbprint '9AA4CA850308B67D
       8F3536434BF4224C5CAC519F' that is specified in the project cannot be found in the certificate store. Please specify a valid thumbprint in the project file. [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj]

    C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VisualStudio\v17.0\AppxPackage\Microsoft.AppXPackage.Targets(2740,5): warning APPX0107: The certificate specified is not valid for signing. For more information about valid certificates, see http://go.microsoft.com/fwlink/?LinkID=241478. [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj]


	"$HOME\source\repos\WSL-DistroLauncher\DistroLauncher.sln" (Build target) (1) ->
	"$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj.metaproj" (default target) (2) ->
	"$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj" (default target) (4) ->
	(_ValidateAppxManifest target) ->
		MyDistro.appxmanifest(14,6): warning APPX0006: This project uses the 'runFullTrust' capability. You should use the Windows Application Packaging Project to produce the store and sideload packages. See https://go.microsoft.com/fwlink/?linkid=871803 for more information. [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj]

Errors start here:

	"$HOME\source\repos\WSL-DistroLauncher\DistroLauncher.sln" (Build target) (1) ->
	"$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj.metaproj" (default target) (2) ->
	"$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj" (default target) (4) ->
	(_GenerateAppxPackageRecipeFile target) ->
		C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Microsoft\VisualStudio\v17.0\AppxPackage\Microsoft.AppXPackage.Targets(3011,5): error APPX0702: Payload file '$HOME\source\repos\WSL-DistroLauncher\x64\install.tar.gz' does not exist. [$HOME\source\repos\WSL-DistroLauncher\DistroLauncher-Appx\DistroLauncher-Appx.vcxproj]

    8 Warning(s)
    1 Error(s)
