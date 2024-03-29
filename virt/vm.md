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
#### KVM (Kernel-based Virtual Machine)  
- - -
- KVM:  
- QEMU: A command-line tool to emulate/virtualize machines/OSs that interacts with other hypervisors such as KVM and can achieve near native performance by executing the guest code directly on the host CPU.  
1. First install the following onto the host:
| Program | Description |
| --- | --- |
| qemu ||
| qemu-system-x86 ||
| virt-manager ||
| virt-viewer ||
| dnsmasq ||
| vde2 ||
| bridge-utils ||
| openbsd-netcat ||
| ebtables ||
| iptables ||
| libguestfs ||

| libvirt-bin ||
| spice-vdagent ||
| qemu-kvm ||
- - -
2. Before you continue, remember to enable virtualization (e.g. VT-x / AMD-V) in your BIOS / UEFI settings.
- Check CPU to see if we have support for vitualization  
`$ grep -E --color 'vmx|svm' /proc/cpuinfo # 'vmx' is for intel and 'svm' is for AMD`  
- - -
3. Start KVM libguestfs
- On Arch based systems:
`$ sudo systemctl enable libvirtd.service`
`$ sudo systemctl start libvirtd.service`
`$ sudo systemctl status libvirtd # Verify virtualization service is running`  
- - -
4. Enable normal user (non-root) to use KVM
`$ sudo vim /etc/libvirt/libvirtd.conf`
- Set the UNIX domain socket group ownership to libvirt, (around line 85)
unix_sock_group = "libvirt"

- Set the UNIX socket permissions for the R/W socket (around line 102)
unix_sock_rw_perms = "0770"

- Add your user account to libvirt group.
`$ sudo usermod -a -G libvirt $(whoami)`
`$ newgrp libvirt`
- Or  
`$ sudo usermod -aG kvm $USER`
`$ sudo usermod -aG libvirt $USER`

- Restart libvirt daemon.
`$ sudo systemctl restart libvirtd.service`
- - -
5. Enable Nested Virtualization (optional)
`$ ### Intel Processor ###`
`$ sudo modprobe -r kvm_intel`
`$ sudo modprobe kvm_intel nested=1`

`$ ### AMD Processor ###`
`$ sudo modprobe -r kvm_amd`
`$ sudo modprobe kvm_amd nested=1`
- To make this configuration persistent, run:
`$ echo "options kvm-intel nested=1" | sudo tee /etc/modprobe.d/kvm-intel.conf`
- Confirm that Nested Virtualization is set to Yes:
`$### Intel Processor ###`
`$ systool -m kvm_intel -v | grep nested`
    `nested              = "Y"`
    `nested_early_check  = "N"`
`$ cat /sys/module/kvm_intel/parameters/nested `
`Y`

`$### AMD Processor ###`
`$ systool -m kvm_amd -v | grep nested`
    `nested              = "Y"`
    `nested_early_check  = "N"`
`$ cat /sys/module/kvm_amd/parameters/nested`
`Y`
- - -
6. Create the new virtual machine via cli  
# virt-install --name=linuxconfig-vm \
--vcpus=1 \
--memory=1024 \
--cdrom=/tmp/debian-9.0.0-amd64-netinst.iso \
--disk size=5 \
--os-variant=debian8
- - -
7. Start virt-manager (GUI option)  
`$ virt-manager`
- - -
###### qemu-system-x86_64
`$ sudo qemu-system-x86_64 -m 512 -enable-kvm -bios /usr/share/edk2-ovmf/x64/OVMF_CODE.fd -usb -device usb-host,hostbus=3,hostaddr=3`

curl -L -O https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/stable-virtio/virtio-win.iso

qemu-img create -f qcow2 win10.qcow2 20G

qemu-system-x86_64 -enable-kvm \
-machine type=q35 \
-m 4G \
-cpu host \
-smp 4 \
-vga virtio \
-device qemu-xhci -device usb-tablet -device usb-kbd \
-device virtio-net,netdev=user0 \
-netdev user,id=user0,hostfwd=tcp::5555-:22 \
-cdrom "$HOME/machines/images/win10_21h1_english_x64.iso" \
-drive file="$HOME/machines/vm/win10.qcow2",index=0,media=disk,if=virtio \
-drive file="$HOME/machines/images/virtio-win.iso",index=3,media=cdrom \
-boot menu=on \
-net nic -net user,hostname=windows1064 \
-name "win10-64"

qemu-img create -f qcow2 archlinux.qcow2 20G

qemu-system-x86_64 -enable-kvm \
-machine type=q35 \
-m 4G \
-cpu host \
-smp 4 \
-vga virtio \
-device qemu-xhci -device usb-tablet -device usb-kbd \
-device virtio-net,netdev=user0 \
-netdev user,id=user0,hostfwd=tcp::5555-:22 \
-cdrom "$HOME/machines/images/archlinux-x86_64.iso" \
-drive file="$HOME/machines/vm/archlinux.qcow2",index=0,media=disk,if=virtio \
-drive file="$HOME/machines/images/virtio-win.iso",index=3,media=cdrom \
-boot menu=on \
-net nic -net user,hostname=archlinux \
-name "archlinux-x86_64"

-snapshot archvm \

###### android-x86:
1. Download latest ISO from android-x86.org
