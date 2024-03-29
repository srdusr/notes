### Arch Linux Installation Guide with optional LUKS (encryption) and/or LVM (Logical Volume Management)  
- - -
0. Optional:
- Useful system information that may help in trouble-shooting.  
`# cat /etc/passwd` # Check all users on the system  
`# cat /etc/shells` # List shells installed on system  
- Installing via ssh (recommended to have prior knowledge of ssh/networking)  
  - Set up the password for root on the remote(target) machine  
  `# passwd`  
  > NOTE: No need to reset password later on during the installation  
  - Connect to the internet by doing Step ***2. Connect to the internet***  
  - Get the IP address (recommended to get both remote and local)  
  `# ip a`  
  or  
  `# ifconfig`  
  > NOTE: Getting the correct IP address will vary in method and might require trial and error.
  A few factors to consider are whether either remote/local are in a VM and if local is a different OS, example Windows would use `# ipconfig`.
  - Confirm that `PermitRootLogin yes` is set in /etc/ssh/sshd_config on the remote machine. If it's not, set it  
  `# vim /etc/ssh/sshd_config`  
  - Reload the sshd daemon on the remote machine  
  `# pkill sshd && /usr/bin/sshd`  
  - Generate keys  
  `# ssh-keygen A`  
  `# ssh-keygen`  
  > NOTE: No need to enter passphrase unless desired.  
  - OpenSSH has a utility to send the key remotely to either machine, only use the `-p` flag if specifying a `<port>` to use  
  `# ssh-copy-id -p <port> -i ~/.ssh/id_rsa.pub user@ip.address`  
  > NOTE: Working out which `<port>` to use (default is usually 22) might also require trial and error dependent on remote/local configurations. Some commands to check current active ports: `lsof -Pi | grep ssh` and `netstat -lntu`.
  - Connect to the target machine on the local machine via ssh  
  `# ssh -p <port> root@ip.address`  
- - -
1. Change keyboard layout (only applicable if not using a pc/laptop US keyboard)
- Look for an appropriate keyboard layout example: `us`  
`# localectl list-keymaps | grep <keymap>`  
- Set the console keyboard layout  
`# loadkeys <keymap>`  
- - -
2. Connect to the internet  
- Test internet connection  
`# ping archlinux.org` # Use Ctrl-c to stop  
or  
`# ip a`  
- If not sure what interfaces are available (wired connection/wifi), use:  
`# ip link`  
- If using a wired connection, it will usually be picked up automatically  
- If using wifi, it will require some additional setting up. Launch `iwctl` prompt:  
`# iwctl`  
- List available devices:  
`[iwd]# device list` # Should see wifi available with a name like `wlan0`, adjust accordingly if necessary  - Scan for networks and list available Wi-Fi networks:  
`[iwd]# station wlan0 scan` # This command outputs nothing  
`[iwd]# station wlan0 get-networks`  
- Connect to wifi network where `<wifi-name>` is the name of the device  
`[iwd]# station wlan0 connect <wifi-name>`  
- Enter the passphrase for wifi  
- Exit the iwctl and don't forget to test the connection again  
`[iwd]# exit`  
- - -
3. Sync system clock, mirrors and servers  
- Update the system clock  
`# timedatectl set-ntp true`  
- Sync the pacman repositories/servers
`# pacman -Syy`
- Update mirror list by installing reflector and running the following command  
`# pacman -S reflector`  
`# reflector -c '<Country>' -a 6 --sort rate --save /etc/pacman.d/mirrorlist`  
- - -
4. Partition the disks  
    4.1. Get information on boot mode and current blocks  
    - Verify the boot mode, the below command must show the directory without error otherwise the system is not booted in UEFI mode  
    `# ls /sys/firmware/efi/efivars`  
    > NOTE if no-UEFI (legacy aka BIOS) system we cannot create LVM partiton(s) therefore if wanting to create more than one partition must create a default linux filesystem in ***4.3.*** and also skip ***4.5.***  
    - List block devices to get the disk name (where disk device is), usually "/dev/sda", "/dev/vda", "/dev/nve0n1" or "/dev/mmcblk0" etc..  
    `# lsblk`  
    > NOTE: From here onwards we'll assume the disk and it's partition's names are `sda`, `sda1` and `sda2` respectively and one must adjust it to their actually names on their system accordingly.  

    4.2. Create the `BIOS` or `UEFI` partition  
    - Create the partition using gdisk (partitioning tool)  
    `# gdisk /dev/sda`  
    - Type `n` for new and press "enter"  
    - Press "enter" on default Partition number  
    - Press "enter" on default First sector  
    - Put in `+512M` on Last sector if using more than one partition (recommended but if `UEFI` then it is required), example: "`/boot` or `/efi` and `/root`" or "`/boot` or `/efi`, `/root` and `/home`" etc... Therefore this will be the `/boot` or `/efi` partition otherwise just press "Enter" and skip ***4.3.*** to create only one partition.  
    > NOTE: `M` is short for megabytes and can be `+300M` or `+1024M`.  
    - Current type:  
      - If `BIOS` just press "enter"  
    - or
      - If `UEFI` put in `ef00` and press "enter" to change the Current type code from Linux filesystem to EFI system partition  

    4.3. Either create one or more seperate default linux filesystem(s) or LVM (recommended)  
    > NOTE: If your filesystem choice is BTRFS later on in ***5. Format the filesystem***, there is no need to create LVMs since it has it's own Subvolume feature. LVM (Logical Volume Management) is useful if we want a flexible disk storage that we either need to create separate partitions on, be able to resize them on the fly or to create snapshots.  
    - Continuing...  
    - Type `n` again to create another new partition and press "enter".  
    - Press "enter" on default Partition number again.  
    > NOTE: The value should correspond with how many partitions we are making. Example should be `default 2` if this is the 2nd partition otherwise put in `2` or whatever correct value needed and press "Enter".  
    - Press "enter" on default First sector again.  
    - Press "enter" on default Last sector this time to use the remaining space if just creating one other partition `/root` or using LVM otherwise if more seperate partitions will be created, example: `/home` and/or `/swap` and/or `/var` then put in a fixed amount of space by repeating step ***4.3.*** for each but make sure to do `/root` last if no seperate `/home` partition or `/home` last if specified and let it have the remaining space by just pressing "Enter". Another option is to specifiy space for the last created partition (`/home`/`/root`) therefore we have leftover unused space to use in the future to possibily allocate to existing or create more partitions.  
    > NOTE: General recommendations:  
    > - `+60G` for `/root` or recommend at least 15-20G, more is better. If `/home` is created then user-data will be stored in `/home`. `/root` will usually store what's installed from the package manager(s) therefore if many packages/software will be installed don't be afraid to increase the size, example `+80G` or more if disk has enough space.  
    > - `+4G` for `/swap` or the general rule of thumb is 1x2 of RAM. Instead of using a `/swap` partition one can use swapfile or  
    > - `+10G` for `/var` or `/var/tmp`  
    - On Current type either:
    > NOTE: LVM requires `UEFI` therefore if `BIOS` then create default filesystem.  
      - Press "enter" if default filesystem (example: `/root`/`/var`/`/home`), if `/swap` then put in `8200`.  
    - or  
      - Put in `8e00` to change the Current type code from Linux filesystem to Linux LVM if using LVM which will be continued in step ***4.5.***  
    - Save changes  
      - Type "w" to write changes and press "enter"  
      - Type "y" to confirm and press "enter"  
    - List block devices again to check the new partitions  
    `# lsblk`  
    > NOTE: Some example partition layouts:  

    BIOS shared partition
    > ```
    > NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS  
    > loop0    7:0    0 702.1M  1 loop /run/archiso/airootfs  
    > sr0     11:0    1 816.3M  0 rom  
    > sr1     11:1    1 153.5M  0 rom  
    > vda    254:0    0    20G  0 disk  
    > └─vda1 254:1    0    20G  0 part  

    `/boot` or `/efi` and `/root`
    > ```
    > NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS  
    > loop0    7:0    0 702.1M  1 loop /run/archiso/airootfs  
    > sr0     11:0    1 816.3M  0 rom  
    > sr1     11:1    1 153.5M  0 rom  
    > vda    254:0    0    20G  0 disk  
    > ├─vda1 254:1    0   512M  0 part  
    > └─vda2 254:2    0  19.5G  0 part  

    `/boot` or `/efi`, `/root`, `/swap` and `/home`  
    > ```
    > NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
    > loop0    7:0    0 702.1M  1 loop /run/archiso/airootfs
    > sr0     11:0    1 816.3M  0 rom
    > sr1     11:1    1 153.5M  0 rom
    > vda    254:0    0    20G  0 disk
    > ├─vda1 254:1    0   512M  0 part
    > ├─vda2 254:2    0     5G  0 part
    > ├─vda3 254:3    0     4G  0 part
    > └─vda4 254:4    0  10.5G  0 part

    `/efi`, LUKS and LVM
    > ```
    > NAME           MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINTS
    > sda              8:0    0 465.8G  0 disk
    > ├─sda1           8:1    0   200M  0 part  /boot
    > └─sda2           8:2    0 465.6G  0 part
    >   └─lvm        254:0    0 465.5G  0 crypt
    >     ├─vg1-root 254:1    0    80G  0 lvm   /
    >     ├─vg1-swap 254:2    0     4G  0 lvm   [SWAP]
    >     └─vg1-home 254:3    0 381.5G  0 lvm   /home
    > sr0             11:0    1  1024M  0 rom

    4.4. (Optional) Encrypt our main partition `sda2` using LUKS  
    - Load dm-crypt and dm-mod kernel modules  
    `# modprobe dm_crypt`  
    `# modprobe dm_mod`  
    - Format the partition using cryptsetup  
    `# cryptsetup luksFormat /dev/sda2`  
    - or  
    - Format the partition and setup a stronger encryption with sha512 LUKS and added randomness  
    `# cryptsetup --cipher aes-xts-plain64 --hash sha512 --use-random --verify-passphrase luksFormat /dev/sda2`  
    - Confirm overwrite by typing in uppercase `YES` and press "enter"  
    - Type in new encryption passphrase  
    - Verify passphrase  
    - Open up partition to create a name for it, create LVMs and format them, example for a name could be `root`  
    `# cryptsetup open /dev/sda2 <name-of-partition>`  
    - Enter passphrase  

    4.5. Continuing with LVM  
    > NOTE: Only continue this step if using LVM, if encrypted use volume path `/dev/mapper/` aka "device mapper" instead of `/dev/sda2`
    - Create physical volumes (PV)  
    `# pvcreate /dev/sda2`  
    - or  
    `# pvcreate /dev/mapper/<name-of-partition>` # if encrypted  
    - Create the volume group (VG) with a `<volume-group-name>` called `vg1` or any other appropriate name on the encrypted volume path  
    > NOTE: From here onwards we'll also assume the `volume-group-name` is `vg1` and one must adjust it accordingly. Always make meaningful volume and volume group names.  
    <!-- -->  
    &emsp;&emsp;`# vgcreate vg1 /dev/sda2`  
    - or  
    `# vgcreate vg1 /dev/mapper/<name-of-partition>` # if encrypted  
    - Create logical volumes (LV) root, swap (optional) and home  
    `# lvcreate -L 40G vg1 -n root` # plan on having a lot of packages installed bump it up maybe to 60gb or 80gb etc..  
    `# lvcreate -L 4G vg1 -n swap` # can be any size between 2gb, 4gb or 8gb  
    `# lvcreate -l 100%FREE vg1 -n home` # give the remaining space to home  
```
  -L        =  absolute size  
  -l        =  left over space  
  100%FREE  =  percentage of free space  
  nG        =  partition size where n is number of and G is gigabytes  
  vg1       =  specify VG name  
  -n        =  name LV  
  <name>    =  name of LV  
```
- - -
5. Format the filesystem
- Check changes and see if everything is correct  
    `# lsblk`  
- Based on what system, UEFI or no-UEFI and if encrypted/LVM do one of these options:  
  - **If no-UEFI (legacy) system**  
    - Without encryption  
        - Format boot partition to EXT4 filesystem  
        `# mkfs.ext4 /dev/sda1`  
        > NOTE: Since only have one root partition just format it by itself.  
      <hr style="border: 0.8 normal; width:100%;"></hr>  
    - With encryption  
        - Format boot partition to EXT4 filesystem  
        `# mkfs.ext4 /dev/sda1`
        - Format encrypted root partition to EXT4 filesystem  
        `# mkfs.ext4 /dev/mapper/<name-of-partition>`  
      <hr style="border: 0.8px normal; width:100%;"></hr>  
  - **If UEFI system**  
    - Without encryption and LVM  
        - Format boot efi partition to FAT32 filesystem  
        `# mkfs.fat -F32 /dev/sda1`  
        - Format root partition to EXT4 filesystem  
        `# mkfs.ext4 /dev/sda2`  
      <hr style="border: 0.8px normal; width:100%;"></hr>  
    - Encryption and without LVM  
        - Format boot efi partition to FAT32 filesystem  
        `# mkfs.fat -F32 /dev/sda1`  
        - Format root partition to EXT4 filesystem  
        `# mkfs.ext4 /dev/mapper/<name-of-partition>`  
      <hr style="border: 0.8px normal; width:100%;"></hr>  
    - LVM and with/without encryption  
        - Format boot efi partition to FAT32 filesystem  
        `# mkfs.fat -F32 /dev/sda1`  
        - Format root and home partition to EXT4 filesystem  
        `# mkfs.ext4 /dev/vg1/root`  
        `# mkfs.ext4 /dev/vg1/home`  
        - Only make swap file partition if it was previously made  
        `# mkswap /dev/vg1/swap`  
- - -
6. Mount the filesystems
 - Check partitions before mounting  
`# lsblk`  
- Make a boot directory in installation directory to mount `/dev/sda1`  
`# mkdir /mnt/boot`  
- Mount efi boot into installation directory  
`# mount /dev/sda1 /mnt/boot`  
- Mount logical volume path of root into installation directory  
`# mount /dev/vg1/root /mnt`  
- Make a home directory in installation directory  
`# mkdir /mnt/home`  
- Mount logical volume path of home into installation directory  
`# mount /dev/vg1/home /mnt/home`  
- Only activate swap on installation directory if it was previously made  
`# swapon /dev/vg1/swap`  
- Check mountpoints are correct  
`# lsblk`  
- - -
7. Install base system  
- First find out what processor the system is using  
`# lscpu`  
- Install base packages  
`# pacstrap /mnt base linux linux-firmware vim amd-ucode lvm2 man openssh tmux`  
> NOTE: If LTS (long-term support) is desired replace `linux` with `linux-lts`. Omit `linux-firmware` if installing in a VM (virtual machine) or container. Replace `vim` with desired text-editor, example `nano`. Replace `amd-ucode` with `intel-ucode` if we have an intel processor. Omit `lvm2` if not using LVM. The packages `man`, `openssh` and `tmux` are optional.  
 - - -
8. Move into installation  
- First generate the fstab file (where mount points are stored) use `-U` or `-L` to define by UUID or labels respectively  
 `# genfstab -U /mnt >> /mnt/etc/fstab`  
- See what is in the fstab file  
 `# cat /mnt/etc/fstab`  
- Move into the installation  
 `# arch-chroot /mnt`  
- - -
9. Configure new system  
- Setting correct live timezone  
 `# ln -sf /usr/share/zoneinfo/<Continent>/<City> /etc/localtime`  
- Synchronize hardware clock to system clock  
 `# hwclock --systohc`  
- Edit locale.gen file, replace vim with text-editor of choice  
 `# vim /etc/locale.gen`  
- Uncomment `en_US.UTF-8 UTF-8` and any other needed locales (LANG variable), save and exit  
- Generate locales  
 `# locale-gen`  
- Also put the chosen locale into locale.conf  
 `# echo LANG=en_US.UTF-8 >> /etc/locale.conf`  
- If chosen a different keyboard layout in the beginning put it into vconsole.conf  
 `# echo KEYMAP=<keymap> >> /etc/vconsole.conf`  
- Hostname (machine's name)  
 `# vim /etc/hostname`  
- Put in desired hostname (name of computer), example: `archlinux`, save and exit  
- Edit host file (/etc/hosts) putting in previously mentioned hostname  
 `# echo "127.0.0.1 localhost" >> /etc/hosts`  
 `# echo "::1       localhost" >> /etc/hosts`  
 `# echo "127.0.1.1 <hostname>.localdomain <hostname>" >> /etc/hosts`  
- Give root user a new password  
 `# passwd`  
> NOTE: No need to create password again if done already, example would be if already set when using ssh.
- Type in new password and retype it to verify  
- Install packages  
  `# pacman -S grub efibootmgr base-devel xdg-utils xdg-user-dirs linux-headers git less networkmanager network-manager-applet wpa_supplicant dialog mtools dosfstools nfs-utils inetutils dnsutils bluez bluez-utils cups hplip alsa-utils pipewire pipewire-alsa pipewire-pulse pipewire-jack rsync reflector acpi acpi_call tlp virt-manager qemu qemu-arch-extra edk2-ovmf bridge-utils dnsmasq vde2 openbsd-netcat iptables-nft ipset firewalld sof-firmware nss-mdns acpid os-prober ntfs-3g xclip`  
- - -
10. Prepare boot loader
- If using a new keymap and/or LVM and/or encryption edit initcpio.conf file and insert the necessary information  
`# vim /etc/mkinitcpio.conf`  
- Look for the "HOOKS" section and after "autodectect" insert `keymap` then after "block" insert `encrypt` and `lvm2`, save and exit.  
> NOTE: Only put in `keymap` if default US keyboard was changed, `encrypt` if encrypted and `lvm2` if using LVM  

   Example:
```
HOOKS=(base udev autodetect keymap modconf block encrypt lvm2 filesystems keyboard fsck)
```
- Generate the initramfs (initial RAM file system) image, replace linux with linux-lts if that was chosen  
`# mkinitcpio -p linux`  
- Install GRUB (boot loader) for either UEFI or no-UEFI  
- For no-UEFI:  
`# grub-install /dev/vda` # And skip to generating config file for file  
- For UEFI:  
`# grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB`  
> NOTE: If above command doesn't work try this rather   

&emsp;&emsp;`# Grub-install - - target=x86_64-efi - - bootloader-id=grub - - efi-directory=/boot/efi`  
- Display block ID (UUID) for "/dev/sda2" and copy it to system clipboard using the command below or omit everything after `blkid` and write it down somewhere else  
`# blkid | grep -oP '/dev/sda2: UUID="\K[^"]+' | xclip -sel clip`  
- Edit GRUB file  
`# vim /etc/default/grub`  
- Go down to `GRUB_CMDLINE_LINUX=""` and insert the following information inbetween the apostrophes:  
`cryptdevice=UUID=</dev/sda2's-UUID>:<name-of-partition> root=/dev/volume-group-name/root`  
  Example:  
```
GRUB_CMDLINE_LINUX="cryptdevice=UUID=f233c213-37e8-4f60-b0bd-a6689ea0cb6c:cryptlvm root=/dev/vg1/root"  
```
- Save and exit  
- Generate configuration file for grub  
`# grub-mkconfig -o /boot/grub/grub.cfg`  
- - -
11. Enable services  
- Enable Network, Bluetooth and Printer services for when the machine is booted  
`# systemctl enable NetworkManager`  
`# systemctl enable bluetooth`  
`# systemctl enable cups.service`  
- - -
12. Create new user with sudo privileges  
- Create a new user  
`# useradd -mG wheel <username>`  
```
useradd  =  add a user
-m       =  associate a home directory
G        =  specify a group
wheel    =  group name
```
- Password for new user  
`# passwd <username>`  
- Type in new password and retype it to verify  
- Enable sudo privileges for any user of the `wheel` group, replace vim with editor of choice  
`# EDITOR=vim visudo`  
- Look for and uncomment `# %wheel ALL=(ALL) ALL`, save and exit  
  Example:  
```
%wheel ALL=(ALL) ALL
```
- - -
13. Reboot new system
- Exit installation and return to the installer  
`# exit`  
- Unmount the partitions  
`# umount -a`  
- Reboot  
`# reboot`  
- Grub boot loader should load, press "enter" to boot the OS  
- If encrypted enter passphrase  
- Login as user with `<username>`, press "enter" and type in the user's password  
- Check for IP  
`$ ip a`  
- Login into wifi  
`$ nmtui`  
- Go to `Activate a connection`, select network to connect to, enter password and quit  

#### Optional Installations  
Install a DE (Desktop Environment)/WM (Window Manager)
- Install yay package manager  
`$ git clone https://aur.archlinux.org/yay.git`  
`$ cd yay`  
`$ makepkg -si PKGBUILD`  
`$ cd`  
`$ rm -rf yay`  


 - Install graphics card drivers  
    - If intel card:  
  `$ sudo pacman -S x86-video-intel`  
    - If amd card:  
  `$ sudo pacman -S x86-video-amdgpu`  
    - If nvidia card:  
    NOTE: First check up on archwiki to see what is supported and methods: https://wiki.archlinux.org/title/NVIDIA  
  `$ sudo pacman -S nvidia nvidia-utils nvidia-settings`  

Package List:
  ` grub efibootmgr base-devel xdg-utils xdg-user-dirs linux-headers git less networkmanager network-manager-applet wpa_supplicant dialog mtools dosfstools nfs-utils inetutils dnsutils bluez bluez-utils cups hplip alsa-utils pipewire pipewire-alsa pipewire-pulse pipewire-jack rsync reflector acpi acpi_call tlp virt-manager qemu qemu-arch-extra edk2-ovmf bridge-utils dnsmasq vde2 openbsd-netcat iptables-nft ipset firewalld sof-firmware nss-mdns acpid os-prober ntfs-3g xclip`  

