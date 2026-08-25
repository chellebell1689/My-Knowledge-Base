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
