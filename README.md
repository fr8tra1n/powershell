Concise powershell profile 
==========

Just to humor the average command line nerd :)

External modules:

<ul>
	<li><a href="https://github.com/tkellogg/Jump-Location">Jump-Location</a> - <a href="http://www.hanselman.com/blog/JumpLocationAChangeDirectoryCDPowerShellCommandThatReadsYourMind.aspx">Hanselman certified</a></li>
	<li><a href="https://pscx.codeplex.com/">PowerShell Community Extensions</a></li>
	<li><a href="https://github.com/lzybkr/PSReadLine">PSReadLine</a> - <a href="http://www.hanselman.com/blog/TowardsABetterConsolePSReadlineForPowerShellCommandLineEditing.aspx">Hanselman certified as well</a></li>
</ul>

```Powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
Import-Module Pscx -arg @{
	TextEditor = 'C:\Program Files\Sublime Text 3\sublime_text.exe'
}
Import-Module 'C:\Program Files (x86)\Jump-Location\Jump.Location.psd1'
Import-Module PSReadLine

#Set environment variables for Visual Studio Command Prompt
pushd 'c:\Program Files (x86)\Microsoft Visual Studio 12.0\VC'
cmd /c "vcvarsall.bat&set" |
foreach {
  if ($_ -match "=") {
    $v = $_.split("="); set-item -force -path "ENV:\$($v[0])"  -value "$($v[1])"
  }
}
popd
write-host "Visual Studio 2012 Command Prompt variables set." -ForegroundColor Yellow
```
