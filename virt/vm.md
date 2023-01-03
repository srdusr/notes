#### Virtualbox  
1. Install the following onto the host:  
virtualbox  
virtualbox-guest-utils  
virtualbox-guest-iso  
virtualbox-host-dkms  
- How to fix Grayed out [ ] Enable Nested VT-x/AMD-V in Settings/System/Processor/Extended Features:  
  ```bash
  $ VBoxManage modifyvm "Virtualbox name" --nested-hw-virt on
  ```
