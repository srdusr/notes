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
1. First install the following onto the host:
| Program | Description |
| --- | --- |
| qemu ||
| virt-manager ||
| virt-viewer ||
| dnsmasq ||
| vde2 ||
| bridge-utils ||
| openbsd-netcat ||
| ebtables ||
| iptables ||
| libguestfs ||
- - -
2. Start KVM libguestfs
- On Arch based systems:
`$ sudo systemctl enable libvirtd.service`
`$ sudo systemctl start libvirtd.service`
- - -
3. Enable normal user (non-root) to use KVM
`$ sudo vim /etc/libvirt/libvirtd.conf`
- Set the UNIX domain socket group ownership to libvirt, (around line 85)
unix_sock_group = "libvirt"

- Set the UNIX socket permissions for the R/W socket (around line 102)
unix_sock_rw_perms = "0770"

- Add your user account to libvirt group.
`$ sudo usermod -a -G libvirt $(whoami)`
`$ newgrp libvirt`

- Restart libvirt daemon.
`$ sudo systemctl restart libvirtd.service`
- - -
