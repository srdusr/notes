timedatectl list-timezones | grep Johannesburg  -- Finding desired timezone
ln -sf /usr/share/zoneinfo/Afica/Johannesburg /etc/localtime -- Setting correct live timezone
#Edit /etc/locale.gen and uncomment en_US.UTF-8 UTF-8 and other needed locales.
locale-gen ## Generate the locales by running

echo LANG=en_US.UTF-8 >> /etc/locale.conf
#Create the locale.conf(5) file, and set the LANG variable accordingly:
/etc/locale.conf

LANG=en_US.UTF-8
hwclock --systohc
ip a -- check for internet connection/ip addr(ess)
ping www.archlinux.com -- check for internet connection part 2
iwctl -- if using wifi
lsblk -- list block
gdisk /dev/sda -- partition disk
n -- create new partition
1 -- default partition number

## enter default for first sector
+300M -- for last sector(efi partition)

ef00 --  change partition type code to EFI system
n -- create second partition number

## all parameters are set to default (press enter 3 times) (first, last sector type code(Current type) )

w -- write(save) table to disk and exit

lsblk -- list information about block devices
mkfs.fat -F32 /dev/sda1 -- make file system partition for boot efi
cryptsetup --cipher aes-xts-plain64 --hash sha512 --use-random --verify-passphrase luksFormat /dev/sda2 ## setup encryption with sha512 luks
crypsetup luksOpen /dev/sda2 *name of encryption partition* ## naming your encryption partition and type your encryption passphrase
mkfs.btrfs /dev/mapper/*name of encryption partition* format the encrypted partition
lsblk -- check changes and see if everything is correct
mount /dev/mapper/*name of encryption partition* /mnt ## mounting the partition and create sub volumes  
cd /mnt ## change directory to /mnt
btrfs subvolume create @ ## create first subvolume as root
btrfs subvolume create @home ## create second subvolume as home
cd ## cd back to root directory
umount /mnt ## unmount
mount -o noatime,space_cache=v2,compress-zstd,ssd,discard=async,subvol=@ /dev/mapper/*name of encryption partition* /mnt ## mount 2 subvolumes with options 'no access time (makes access time of disk a little bit faster)', 'use space cache with version 2 since ver 1 doesn't work', 'compresstion method is zstd', 'ssd option if you have one', 'discard to optimize performance of the ssd' and use 'subwool to make sure this volume is equal to the roots of volume first' and then define the mapper device
mkdir /mnt/{boot,home} ##create both at once
mount -o noatime,space_cache=v2,compress-zstd,ssd,discard=async,subvol=@home /dev/mapper/*name of encryption partition* /mnt/home
mount /dev/sda1 /mnt/boot
pacstap /mnt base linux linux-firmware git vim man networkmanager
genfstab -U /mnt >> /mnt/etc/fcstab
arch-chroot /mnt
vim /etc/mkinitcpio.conf
## under modules ##
-- MODULES=(btrfs)
## put encrypt between block and filesystems
HOOKS=(base udev autodetect modconf block encrypt filesystems keyboard fsck)


echo "arch" >> /etc/hostname
echo "127.0.0.1 localhost" >> /etc/hosts
echo "::1       localhost" >> /etc/hosts
echo "127.0.1.1 arch.localdomain arch" >> /etc/hosts
passwd # then enter your root password and verify it

pacman -S grub efibootmgr networkmanager network-manager-applet dialog wpa_supplicant mtools dosfstools base-devel linux-headers avahi xdg-user-dirs xdg-utils gvfs gvfs-smb nfs-utils inetutils dnsutils bluez bluez-utils cups hplip alsa-utils pipewire pipewire-alsa pipewire-pulse pipewire-jack bash-completion openssh rsync reflector acpi acpi_call tlp virt-manager qemu qemu-arch-extra edk2-ovmf bridge-utils dnsmasq vde2 openbsd-netcat iptables-nft ipset firewalld flatpak sof-firmware nss-mdns acpid os-prober ntfs-3g terminus-font
