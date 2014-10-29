Concise powershell profile 
==========

Just to humor the average command line nerd :)

External modules:

<ul>
	<li><a href="https://github.com/tkellogg/Jump-Location">Jump-Location</a> - <a href="http://www.hanselman.com/blog/JumpLocationAChangeDirectoryCDPowerShellCommandThatReadsYourMind.aspx">Hanselman certified</a></li>
	<li><a href="https://pscx.codeplex.com/">PowerShell Community Extensions</a></li>
	<li><a href="https://github.com/lzybkr/PSReadLine">PSReadLine</a> - <a href="http://www.hanselman.com/blog/TowardsABetterConsolePSReadlineForPowerShellCommandLineEditing.aspx">Hanselman certified as well</a></li>
	<li><a href="http://blogs.technet.com/b/windowsserver/archive/2014/04/03/windows-management-framework-v5-preview.aspx">Windows Management Framework v5 preview</a> (this includes the <a href="https://github.com/OneGet/oneget">OneGet</a> package manager)</li>
</ul>

```Powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
Import-Module Pscx -arg @{
	TextEditor = 'C:\Program Files\Sublime Text 3\sublime_text.exe'
}
Import-Module 'C:\Program Files (x86)\Jump-Location\Jump.Location.psd1'
Import-Module PSReadLine
Import-Module –Name OneGet

#Set environment variables for Visual Studio Command Prompt
pushd 'c:\Program Files (x86)\Microsoft Visual Studio 12.0\VC'
cmd /c "vcvarsall.bat\&set" |
foreach {
  if ($_ -match "=") {
    $v = $_.split("="); set-item -force -path "ENV:\$($v[0])"  -value "$($v[1])"
  }
}
popd
write-host "Visual Studio 2012 Command Prompt variables set." -ForegroundColor Yellow

#ps version
write-host "PowerShell $($PSVersionTable.PSVersion.ToString())" -ForegroundColor Yellow
```
