
- Update system
`# pacman -Syu`

- Change password of root
`# passwd`

- Configure new system  
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

- Install common base tools
`# pacman -S vim sudo visudo wget networkmanager xorg xorg-server git openssh fakeroot base-devel tigervnc tmux neofetch`

- Create new user with sudo privileges  
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

- Add <username> to sudoers. Edit/etc/sudoers with vi, add following lines beneath "root ALL=(ALL) ALL":
`<username> ALL=(ALL) ALL`

- Login to the non-root user account by default,
`# echo startarch login username > archlinux; chmod +x archlinux`

- To login into account:
`$ ./archlinux`

- Install yay
`$ sudo pacman -S --needed git base-devel && git clone https://aur.archlinux.org/yay.git && cd yay && makepkg -si`
