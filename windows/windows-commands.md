#### <u>Shutdown Options</u>  
- Restart computer into BIOS  
  `shutdown /r /fw /f /t 0`  
- Shutdown  
  `shutdown /s`  
- Restart  
  `shutdown /r`  
- - -
#### <u>BCDEdit (Boot Configuration Data) Command-line Options</u>  
- Enable safe mode via commandline  
 `bcedit /set {default} bootmenupolicy legacy`  
- Disable hyper-v  
  `bcdedit /set hypervisorlaunchtype off`  
- Enable hyper-v  
  `bcdedit /set hypervisorlaunchtype auto`  
- - -
