## Code to download all the Dynamics CRM solution packer tools
<br />## In C drive and creat a folder called SolutionPackagerDemo
<br />## Dowload either managed/unmanaged solution and store it the above folder
<br />## Log in to windows powershell ISO and cd to root then cd to the above folder
<br /##> Now copy the code

<br />## To Unpack/Extract use `solutionpackager.exe/action:Extract/zipfile:"C:\SolutionPackagerDemo\WomenLiftTheme_1_0_0_1.zip"\folder:"C:\SolutionPackagerDemo\ExtractedSoln"`
<br />## To Pack use <br /> `solutionpackager.exe /action:Pack /folder:"C:\SolutionPackagerDemo\ExtractedSoln" /zipfile:ZippedSolnFolder.zip"`

solutionpackager.exe /action:Pack /folder:"C:\SolutionPackagerDemo\ExtractedSoln" /zipfile:ZippedSolnFolder.zip"
##


[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
$sourceNugetExe = "https://dist.nuget.org/win-x86-commandline/latest/nuget.exe"
$targetNugetExe = ".\nuget.exe"
Remove-Item .\Tools -Force -Recurse -ErrorAction Ignore
Invoke-WebRequest $sourceNugetExe -OutFile $targetNugetExe
Set-Alias nuget $targetNugetExe -Scope Global -Verbose

##
##Download Plug-in Registration tool
##
./nuget install Microsoft.CrmSdk.XrmTooling.PluginRegistrationTool -O .\Tools
md .\Tools\PluginRegistration
$prtFolder = Get-ChildItem ./Tools | Where-Object {$_.Name -match 'Microsoft.CrmSdk.XrmTooling.PluginRegistrationTool.'}
move .\Tools\$prtFolder\tools\*.* .\Tools\PluginRegistration
Remove-Item .\Tools\$prtFolder -Force -Recurse

##
##Download CoreTools
##
./nuget install  Microsoft.CrmSdk.CoreTools -O .\Tools
md .\Tools\CoreTools
$coreToolsFolder = Get-ChildItem ./Tools | Where-Object {$_.Name -match 'Microsoft.CrmSdk.CoreTools.'}
move .\Tools\$coreToolsFolder\content\bin\coretools\*.* .\Tools\CoreTools
Remove-Item .\Tools\$coreToolsFolder -Force -Recurse

##
##Download Configuration Migration
##
./nuget install  Microsoft.CrmSdk.XrmTooling.ConfigurationMigration.Wpf -O .\Tools
md .\Tools\ConfigurationMigration
$configMigFolder = Get-ChildItem ./Tools | Where-Object {$_.Name -match 'Microsoft.CrmSdk.XrmTooling.ConfigurationMigration.Wpf.'}
move .\Tools\$configMigFolder\tools\*.* .\Tools\ConfigurationMigration
Remove-Item .\Tools\$configMigFolder -Force -Recurse

##
##Download Package Deployer 
##
./nuget install  Microsoft.CrmSdk.XrmTooling.PackageDeployment.WPF -O .\Tools
md .\Tools\PackageDeployment
$pdFolder = Get-ChildItem ./Tools | Where-Object {$_.Name -match 'Microsoft.CrmSdk.XrmTooling.PackageDeployment.Wpf.'}
move .\Tools\$pdFolder\tools\*.* .\Tools\PackageDeployment
Remove-Item .\Tools\$pdFolder -Force -Recurse

##
##Remove NuGet.exe
##
Remove-Item nuget.exe
