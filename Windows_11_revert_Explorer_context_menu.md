# Windows 11 revert Explorer context menu
Right-click the Start button and choose Windows Terminal.
Copy the command from below, paste it into Windows Terminal Window, and press enter.
```
reg.exe add "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32" /f /ve
```
Restart File Explorer or your computer for the changes to take effect.