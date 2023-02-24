#### Virtualbox  
- - -
1. First install the following onto the host:  

| Program | Description |
| --- | --- |
| virtualbox||  
| virtualbox-guest-utils | |  
| virtualbox-guest-iso | |  
| virtualbox-host-dkms | VirtualBox Host kernal modules sources |  
- - -
2. Recommend to verify 3D acceleration is enabled/supported on host  
- On Linux:  
Make sure mesa-utils package is installed so we can use tools like **glxinfo** and **glxgears**  
  - Check for direct rendering  
`$ glxinfo | grep "direct rendering"` # Value should be **Yes** to indicate 3D acceleration is enabled  
  - Test framerate/3D acceleration  
`$ glxgears` # Framerate should be approximately the same as the monitor refresh rate  
&emsp;
- - -
- Enable safe mode via commandline in a windows guest  
 `bcedit /set {default} bootmenupolicy legacy`  
- Download guest additions in windows guest  
  http://download.virtualbox.org/virtualbox/
vboxmanage modifyvm "win10" --accerlerate3d on
- To check VM log file in case of errors. Make sure the VM is fully shut down, then right click it in the manager UI. Select "Show Log" and optionally save "VBox.log"  

- How to fix Grayed out [ ] Enable Nested VT-x/AMD-V in Settings/System/Processor/Extended Features:  
  ```bash
  $ VBoxManage modifyvm "Virtualbox name" --nested-hw-virt on
  ```
- - -
#### KVM  
- - -

- - -
