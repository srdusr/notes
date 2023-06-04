
- Update system
`# pacman -Syu`

- Change password of root
`# passwd`

- Configure new system  
- Setting correct live timezone  
 `# ln -sf /usr/share/zoneinfo/<Continent>/<City> /etc/localtime`  
- Edit locale.gen file, replace vim with text-editor of choice  
 `# vim /etc/locale.gen`  
- Uncomment `en_US.UTF-8 UTF-8` and any other needed locales (LANG variable), save and exit  
- Generate locales  
 `# locale-gen`  
- Also put the chosen locale into locale.conf  
 `# echo LANG=en_US.UTF-8 >> /etc/locale.conf`  

- Install common base tools
`# pacman -S vim sudo visudo wget networkmanager xorg xorg-server git openssh fakeroot bsdtar base-devel tigervnc tmux neofetch`

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

//- Add <username> to sudoers. Edit/etc/sudoers with vi, add following lines beneath "root ALL=(ALL) ALL":
//`<username> ALL=(ALL) ALL`

- Login to the non-root user account by default,
`# echo startarch login username > archlinux; chmod +x archlinux`

- To login into account:
`$ ./archlinux`

- Install yay
`$ sudo pacman -S --needed git base-devel && git clone https://aur.archlinux.org/yay.git && cd yay && makepkg -si`

- Edit ~/.profile and add the following lines:
```bash
export DISPLAY=:0
# Start pulse audio server in proot after login
export PULSE_SERVER=127.0.0.1 && pulseaudio --start --disable-shm=1 --exit-idle-time=-1
```
- or just type this one time:
`$ export DISPLAY=":1"`

- And make it executable
`$ chmod +x ~/.profile`

- Setup vncserver
`$ vncserver -localhost`

- Starting a vncserver, the ports starts from 5900.
`$ vncserver :1`

- Launch RealVNC Viewer, add new connection `localhost:5901` or `127.0.0.1:5901` and type in password to connect to the vncserver
> NOTE: To determine port number on which VNC server listens. It can be calculated by: 5900 + {display number}. So for display 'localhost:1' the port will be 5901

- Make the vnc startup script
`$ mkdir ~/.vnc && touch ~/.vnc/xstartup`

- Edit the startup script
`$ vim ~/.vnc/xstartup`
```bash
#!/data/data/com.termux/files/usr/bin/sh

## file is executed during VNC server
## startup.

# Launch terminal emulator Aterm.
# Requires package 'aterm'.
aterm -geometry 80x24+10+10 -ls &

unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS

export PULSE_SERVER=127.0.0.1 && pulseaudio --start --disable-shm=1 --exit-idle-time=-1

# Execute XFCE4
# Launch Window Manager/Desktop Environment
bspwm &

```
- Make it executable
`$ chmod +x ~/.vnc/xstartup`

- - -

- Trouble-shooting
`# pacman-key --init`
`# pacman-key --populate`
`# pacman -S archlinuxarm-keyring`
`# pacman-key --populate archlinuxarm`
`# rm /var/lib/pacman/db.lck`

