Enable-PSRemoting -SkipNetworkProfileCheck -Force;Set-Service WinRM -StartupType Automatic;Start-Service WinRM;Set-Item WSMan:\localhost\Service\Auth\Basic $false;Set-Item WSMan:\localhost\Service\AllowUnencrypted $false;Get-NetFirewallRule -Name 'WINRM-HTTP-In-TCP*' -ErrorAction SilentlyContinue|Disable-NetFirewallRule;New-NetFirewallRule -Name KISS-XDR-WinRM -DisplayName KISS-XDR-WinRM -Direction Inbound -Action Allow -Protocol TCP -LocalPort 5985 -RemoteAddress 10.2.73.19,10.2.73.24 -Profile Any


Get-NetConnectionProfile | Where-Object NetworkCategory -eq 'Public' | Set-NetConnectionProfile -NetworkCategory Private


Enable-PSRemoting -SkipNetworkProfileCheck -Force
Set-Item WSMan:\localhost\Service\AllowUnencrypted $false
