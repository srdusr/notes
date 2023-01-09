### Arch Linux Installation with optional LUKS (encryption) on LVM (Logical Volume Management)  
- Look for an appropriate keyboard layout  
`# localectl list-keymaps | grep US`  
- Set the console keyboard layout  
`# loadkeys en_US.UTF-8`  
- Verify the boot mode, the below command must show the directory without error otherwise the system is not booted in UEFI mode  
`# ls /sys/firmware/efi/efivars`  
- Test internet connection  
`# ip a`  
- Press "enter" and select wifi and enter password  
`# wifi-menu`  
- Update the system clock  
`# timedatectl set-ntp true`  
- Update mirror list by installing reflector and running the following command  
`# pacman -Syy reflector`  
`# reflector -c <Country> -a 6 --sort rate --save /etc/pacman.d/mirrorlist`  
- Update servers  
`pacman -Syy`  
- List block devices to get the disk-name, usually "sda", "vda" or "nvme01" etc..  
`# lsblk`
- Create EFI Partition using gdisk (partitioning tool)  
`# gdisk /dev/<disk-name>`  
  - Type `n` for new and press "enter"  
  - Press "enter" on default Partition number  
  - Press "enter" on default First sector  
  - `+300M` -- On Last sector (efi partition)  
  - `ef00` -- Change the Current type code from Linux filesystem to EFI system partition and don't do anything else yet  
- Either create a default linux filesystem or LVM (recommended)  
NOTE: If your filesystem choice is BTRFS much later on, there is no need to create LVMs since it has it's own Subvolume feature. LVM (Logical Volume Management) is useful if we want a flexible disk storage that we either need to create separate partitions on, be able to resize them on the fly or to create snapshots.  
- Continuing...  
    - For default filesystem press "enter" 4 times on all parameters (Partition number, First sector, Last sector and Current type)  
    or  
    - Create LVM partition  
      - Type `n` for new again and press "enter"  
      - Press "enter" on default Partition number again  
      - Press "enter" on default First sector again  
      - Press "enter" on default Last sector this time  
      - `8e00` -- Change the Current type code from Linux filesystem to Linux LVM  
- Save changes  
  - Type "w" to write changes and press "enter"  
  - Type "y" to confirm and press "enter"  
- List block devices again to check the new partitions  
  `# lsblk`  
NOTE: From here onwards we'll assume the disk and it's partition's names are sda, sda1 and sda2 respectively and one must adjust it to their actually names on their system accordingly.  
- (Optional) Encrypt our main partition (sda2) using LUKS  
  - Format the partition using cryptsetup  
  `# cryptsetup luksFormat /dev/sda2`  
  or  
  - Format the partition and setup a stronger encryption with sha512 LUKS and added randomness  
  `# cryptsetup --cipher aes-xts-plain64 --hash sha512 --use-random --verify-passphrase luksFormat /dev/sda2`  
  - If an error occurs try this  
  `# modprobe dm_crypt`
  - Type `YES` to confirm overwrite press "enter"  
  - Type in new encryption passphrase  
  - Verify passphrase  
  - Open up partition to create a name for it, create LVMs and format them  
  `# cryptsetup open /dev/sda2 <name-of-partition>`  
  - Enter passphrase  
  - Create physical volumes (PV) on the encrypted volume path "/dev/mapper/"  
    (device mapper)  
  `# pvcreate /dev/mapper/<name-of-partition>`  
  - Create the volume group (VG) with the name "vg1" or any other appropriate name on the encrypted volume path  
  NOTE: Always make meaningful volume and volume group names.  
  `# vgcreate vg1 /dev/mapper/<name-of-partition>`  
  - Create logical volumes (LV) root, swap (optional) and home  
  `# lvcreate -L 40G vg1 -n root` -- plan on having a lot of packages installed bump it up maybe to 60gb or 80gb etc..  
  `# lvcreate -L 4G vg1 -n swap` -- can be any size between 2gb, 4gb or 8gb  
  `# lvcreate -l 100%FREE vg1 -n home` -- give the remaining space to home  
```
  -L        =  absolute size  
  -l        =  left over space  
  100%FREE  =  percentage of free space  
  nG        =  partition size where n is number of and G is gigabytes  
  vg1       =  specify VG name  
  -n        =  name LV  
  <name>    =  name of LV  
```

 - Check changes and see if everything is correct  
  `# lsblk`  
 - Format boot efi partition "/dev/sda1" to FAT32 filesystem  
  `# mkfs.fat -F32 /dev/sda1`  
 - Format root partition "dev/vg1/root" to EXT4 filesystem  
  `# mkfs.ext4 /dev/vg1/root`  
 - Format home partition "dev/vg1/home" to EXT4 filesystem  
  `# mkfs.ext4 /dev/vg1/home`  
 - Only make swap file partition "dev/vg1/swap" if it was previously made (optional)  
  `# mkswap /dev/vg1/swap`  
 - Check partitions before mounting  
  `# lsblk`  
 - Make a boot directory in installation directory to mount "/dev/sda1"  
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
   (optional)  
  `# swapon /dev/vg1/swap`  
 - Check mountpoints are correct  
  `# lsblk`  
 - Install base packages  
 NOTE: If LTS (long-term support) is desired replace linux with linux-lts. Omit linux-firmware if installing in a VM (virtual machine) or container. Replace vim with desired text-editor. Replace intel-ucode with amd-ucode if we have an amd processor. Omit lvm2 if not using LVM.  
  `# pacstrap /mnt base linux linux-firmware vim lvm2 git man openssh tmux`  
  or get a normal base installation with common programs  
  `# pacstrap -i /mnt base base-devel`  
 - Generate the fstab file (where mount points are stored) use `-U` or `-L` to define by UUID or labels respectively  
  `# genfstab -U /mnt >> /mnt/etc/fstab`  
 - See what is in the fstab file  
  `# cat /mnt/etc/fstab`  
 - Move into the installation  
  `# arch-chroot /mnt`
 - Localization of timezone, find nearest timezone  
  `# timedatectl list-timezones | grep <City>`  
 - Setting correct live timezone  
  `# ln -sf /usr/share/zoneinfo/<Continent>/<City> /etc/localtime`  
 - Synchronize hardware clock to system clock  
  `# hwclock --systohc`  
 - Edit locale.gen file, replace vim with text-editor of choice  
  `# vim /etc/locale.gen`  
 - Uncomment `en_US.UTF-8 UTF-8` and any other needed locales (LANG variable), save and exit  
 - Generate the locales by running  
  `# locale-gen`  
 - Also put the chosen locale into locale.conf  
  `# echo LANG=en_US.UTF-8 >> /etc/locale.conf`  
 - If chosen a different keyboard layout in the beginning put it into vconsole.conf  
  `# echo KEYMAP=<keymap> >> /etc/vconsole.conf`  
 - Hostname (machine's name)  
  `# vim /etc/hostname`  
 - Put in desired hostname, example: `archlinux`, save and exit  
 - Edit host file (/etc/hosts) putting in previously mentioned hostname  
  `# echo "127.0.0.1 localhost" >> /etc/hosts`  
  `# echo "::1       localhost" >> /etc/hosts`  
  `# echo "127.0.1.1 <hostname>.localdomain <hostname>" >> /etc/hosts`  
 - Give root user a new password  
  `# passwd`  
- Type in new password and retype it to verify  
- Install packages  
  `pacman -S grub efibootmgr base-devel xdg-utils xdg-user-dirs linux-headers networkmanager network-manager-applet wpa_supplicant dialog mtools dosfstools nfs-utils inetutils dnsutils bluez bluez-utils cups hplip alsa-utils pipewire pipewire-alsa pipewire-pulse pipewire-jack rsync reflector acpi acpi_call tlp virt-manager qemu qemu-arch-extra edk2-ovmf bridge-utils dnsmasq vde2 openbsd-netcat iptables-nft ipset firewalld sof-firmware nss-mdns acpid os-prober ntfs-3g xclip`  
- If using a new keymap and/or LVM and/or encryption edit initcpio.conf file and insert the necessary information  
  `# vim /etc/mkinitcpio.conf`  
- Look for the "HOOKS" section and after "autodectect" insert `keymap` then after "block" insert `encrypt` and `lvm2`, save and exit.  
   Example:
```
HOOKS=(base udev autodetect keymap modconf block encrypt lvm2 filesystems keyboard fsck)
```
- Generate the initramfs (initial RAM file system) image, replace linux with linux-lts if that was chosen  
    `# mkinitcpio -p linux`  
- Install GRUB (boot loader)  
 `# grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB`  
 NOTE: If above command doesn't work try this rather  
 `# Grub-install - - target=x86_64-efi - - bootloader-id=grub - - efi-directory=/boot/efi`  
- Display block ID (UUID) for "/dev/sda2" and copy it using the command below or omit everything after `blkid` and write it down somewhere  
 `# blkid | grep -oP '/dev/sda2: UUID="\K[^"]+' | xclip -sel clip  
- Edit GRUB file  
 `# vim /etc/default/grub`  
- Go down to `GRUB_CMDLINE_LINUX=""` and insert inbetween the apostrophes:  
  `cryptdevice=UUID=</dev/sda2's-UUID>:<name-of-partition> root=/dev/volume-group-path-name/root`  
  Example:  
```
GRUB_CMDLINE_LINUX="cryptdevice=UUID=f233c213-37e8-4f60-b0bd-a6689ea0cb6c:cryptlvm root=/dev/vg1/root"  
```
- save and exit  
- Generate configuration file for grub  
  `# grub-mkconfig -o /boot/grub/grub.cfg`  
- Enable Network, Bluetooth and Printer services for when the machine is booted  
  `# systemctl enable NetworkManager`  
  `# systemctl enable bluetooth`  
  `# systemctl enable cups.service`  
- Create a new user, `-m` is associate a home directory and `G` is the group the user will belong to being the `wheel` group  
   `useradd -mG wheel <username>`  
- Password for new user  
  `# passwd <username>`  
- Type in new password and retype it to verify  
- Enable sudo privileges for any user of the `wheel` group, replace vim with editor of choice  
  `# EDITOR=vim visudo`  
- Look for and uncomment `# %wheel ALL=(ALL) ALL`, save and exit  
- Exit installation and return to the installer  
  `# exit`  
- Unmount the partitions  
 `# umount -a`  
- Reboot  
 `# reboot`  
- Grub boot loader should load, press "enter" to boot the OS  
- If encrypted enter passphrase  
- Login as user with <username> and it's password  
- Check for IP  
 `$ ip a`  
- Login into wifi  
 `$ nmtui`  
 - Go to `Activate a connection`, select network to connect to, enter password and quit  


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


