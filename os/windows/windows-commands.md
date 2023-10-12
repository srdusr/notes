#### <u>Shutdown Options</u>

- Restart computer into BIOS  
```dos
shutdown /r /fw /f /t 0
```
- Shutdown  
```dos
shutdown /s
```
- Restart  
```dos
shutdown /r
```

---

#### <u>BCDEdit (Boot Configuration Data) Command-line Options</u>

- Enable safe mode via commandline  
```dos
bcedit /set {default} bootmenupolicy legacy
```
- Disable hyper-v  
```dos
bcdedit /set hypervisorlaunchtype off
```
- Enable hyper-v  
```dos
bcdedit /set hypervisorlaunchtype auto
```

---

#### <u>Disable Run Privileges bell</u>

- Turn off beeping
```cmd
net stop beep
```
> NOTE: Replace `stop` with `start` to allow the service to work again. Defaults back to on at startup.
- Too disable at startup
  - cmd:
  ```cmd
  sc config beep start= disabled
  ```
  > NOTE: Replace `disabled` with `auto` to allow at startup
  - powershell:
  ```powershell
  set-service beep -startuptype disabled
  ```
  > NOTE: Replace `disabled` with `automatic` to allow at startup

---

#### <u>Allow script execution</u>

- Run the following command in PowerShell as an administrator:

```dos
  Set-ExecutionPolicy RemoteSigned
```

---
