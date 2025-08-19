```powershell
Net stop w32time
W32tm  /unregister
W32tm /register
Net start w32time

Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Parameters" -Name "Type" -Value "NTP" -Type String
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config" -Name "AnnounceFlags" -Value "10" -Type DWord
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpServer" -Name "Enabled" -Value "1" -Type DWord
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Parameters" -Name "NtpServer" -Value "0.pool.ntp.org,0x1 1.pool.ntp.org,0x1 2.pool.ntp.org,0x1 3.pool.ntp.org,0x1" -Type String
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config" -Name "MaxPosPhaseCorrection" -Value "3600" -Type DWord
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\W32Time\Config" -Name "MaxNegPhaseCorrection" -Value "3600" -Type DWord

net stop w32time
net start w32time
w32tm /resync /nowait
w32tm /query /status
w32tm /query /peers
```
