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
- - -
#### Reload a program from tty if gui becomes unresponsive 
  `$ DISPLAY=:<n> <name of program>`  
  Example:  
```
  `$ DISPLAY=:0 xterm &`  
  `$ DISPLAY=:0 sxhkd &`  
```
- - -
