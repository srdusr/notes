## Useful troubleshooting commands/tools

#### Internet/network:

- ifconfig (install net-tools)
  - Manage interface configurations/parameters
  - Enable/disable a network interface
  - View all available interfaces, IP addresses, hardware addresses
  - Assign an IP address and netmask to a selected interface
- ip
  - Alternate to ifconfig, display network interfaces and configure network devices
  - Interact with layers of TCP/IP protocol (Data link layer and Network layer)
  - Can show and modify kernal routing tables (+/- ARP cache entries)

---

#### Reload a program from tty if gui becomes unresponsive

```bash
$ DISPLAY=:<n> <name of program>
```

Example:

```bash
$ DISPLAY=:0 xterm &
$ DISPLAY=:0 sxhkd &
```

---

#### Fix pacman keyring errors

```bash
$ pacman-key --init && pacman-key --populate archlinuxarm
$ rm /var/lib/pacman/db.lck
```

---

#### Clean package manager's cache (apt/pacman)

apt:

```bash
$ sudo apt-get clean
$ sudo apt-get autoclean
```

pacman:

```bash
$ paccache -r # requires pacman-contrib
$ sudo pacman -Scc
```

---

#### Unlocking a Linux User Account After Too Many Failed Attempts

```bash
$ faillock --user $USER --reset
```

---

#### Find top 10 largest files

```bash
$ find /path/to/dir/ -printf '%s %p\n'| sort -nr | head -10
$ find . -printf '%s %p\n'| sort -nr | head -10
```
