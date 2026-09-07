# Printer Related

Stop/start the printer spooler 
```
net stop spooler
net start spooler
```
_net start/stop can be used with any service, use /y when stopping services with dependent services_
_When starting a service with dependents, each dependent must be individually started_


Clear the printer spooler folder (spooler must be stopped while doing this)
```
del %systemroot%\System32\spool\printers\* /Q
```
_Note, use && between commands to concatenate and run multiple commands at once_
_(i.e. net stop spooler && del %systemroot%\System32\spool\printers\* /Q && net start spooler_

============================================================================================

# Scan Related

This is a full scan of all components and drives on the device.  Do these in order and restart after submitting the check disk command
```
Dism.exe /online /Cleanup-Image /checkhealth 
Dism.exe /online /Cleanup-Image /scanhealth 
sfc /scannow 
Dism.exe /online /Cleanup-Image /Restorehealth 
Dism.exe /Online /Cleanup-Image /AnalyzeComponentStore 
Dism.exe /Online /Cleanup-Image /StartComponentCleanup
chkdsk /f /r /x
```
Network-related commands
```
ipconfig /all
ipconfig /release && ipconfig /renew
ipconfig /flushdns && ipconfig /registerdns
nslookup [specific domain] [optional: specific dns server]
tracert [ip address]
route print
```

Grab public IP address for a domain
```
curl ipecho.net/plain
```

Turn off the Windows Defender Firewall _(ONLY USE IF THERE'S A 3rd Party AV IN PLACE)_
```
netsh advfirewall set allprofiles stat off
```

============================================================================================

# Time related Commands

Find where the device is syncing time & force time sync
```
w32tm /query /source
w32tm /resync
```

Set the device to sync time with the NTP  server
```
w32tm /config /manualpeerlist:"time.windows.com,0x8" /syncfromflags:manual /update
```
_You can use this same command to sync with a server on the network by replacing what's between the " " with the server name_
_NOTE: it cannot sync with a vm, MUST be a physical machine or the NTP server_

See the current device time & set new time
```
time [hh:mm:ss]
```
_Just using time will show the current time, but hit the enter key twice_

============================================================================================

# Power management commands (sleep/hibernate/etc)
```
powercfg-chang-standby-timeout-dc 0
powercfg-chang-standby-timeout-ac 0
powercfg-h off
```


# Shutdown commands
```
shutdown /r/t [delay time in seconds]
shutdown /r/f
shutdown /s
shutdown /
shutdown -a
```
_Explination in order: reboot after set time | force reboot now | shutdown now | check shutdown/reboot sched time | cancel last restart/shutdown command_

============================================================================================

# Net (or general) Commands

Show connected drives & map persistent drives
```
net use
net use [drive letter] [drive path] /persistent:yes
```

List contents of a folder & subfolders w/ size (in bytes) for the specified folder and the items in it
```
dir "[path]" /s
```

Turn off Defender Firewall (only if 3rd party firewall is present)
```
netsh advfirewall set allprofiles state off
```
Add local user & add them as a local admin
```
net user [username] [password] /add
net localgroup administrators /add [username]
```
_Use the net user command (with out the /add) to reset the local password_
_Use /delete instead of /add to remove the account from the admin group_

Pull account information for a local account
```
net user [username]
```
_Use /domain to switch to a domain account_
_Use "quotation marks" around the username if it contains a space_

Unlock an account (works w/ domain account too)
```
net user [username] /active:yes
```

Set the password to blank or set the password not to be required
```
net user [username] ""
net user [username] /passwordreq:no
```

Enable/Disable log on for the device/server (very useful when trying to keep users from logging into a host)
```
change logon /disable
change logon /enable
```

Clear the exchange/explorer cache, mostly for issues with Outlook
```
RunDll32.exe InetCpl.cpl,ResetIEtoDefaults
```

