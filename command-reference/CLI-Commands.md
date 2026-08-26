#Printer Related#

Stop/start the printer spooler 
```
net stop spooler
net start spooler
```

Clear the printer spooler folder (spooler must be stopped while doing this)
```
del %systemroot%\System32\spool\printers\* /Q
```
_Note, use && between commands to concatenate and run multiple commands at once_
_(i.e. net stop spooler && del %systemroot%\System32\spool\printers\* /Q && net start spooler_


#Scan Related#

This is a full scan of all components on the device.  Do these in order and restart after submitting the check disk command
```
Dism.exe /online /Cleanup-Image /checkhealth 
Dism.exe /online /Cleanup-Image /scanhealth 
sfc /scannow 
Dism.exe /online /Cleanup-Image /Restorehealth 
Dism.exe /Online /Cleanup-Image /AnalyzeComponentStore 
Dism.exe /Online /Cleanup-Image /StartComponentCleanup
chkdsk /f /r /x
```

#Net (or general) Commands

Show connected drives
```
net use
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

Pull account information for a local account
```
net user [username]
```
_Use /domain to switch to a domain account_
