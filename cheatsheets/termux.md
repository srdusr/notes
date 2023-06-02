- Change password of root
`# passwd`

- 
`# pacman -S sudo vim visudo`

- 
`# passwd <username>`

- Add <username> to sudoers. Edit/etc/sudoers with vi, add following lines beneath "root ALL=(ALL) ALL":
`<username> ALL=(ALL) ALL`

- Login to the non-root user account by default,
`# echo startarch login username > archlinux; chmod +x archlinux`

- To login into account:
`$ ./archlinux`
