### SSH (Secure Shell Protocol)  
* Find out your username  
`whoami`  

* Check ip address  
`ifconfig`  
`nmcli -p device show`  

* Termux install openssh  
`pkg in openssh`  

* Termux make sure user/root password is set  
`passwd <user> # root does not need to be specified`  

* Generate your ssh key pair on remote host machine, not on server machine  
`ssh-keygen`  

* Accessing termux user environment from other consoles  
`scp your_desktop_ssh_user@YOUR.DESKTOP.IP.ADDRESS:~/.ssh/id_rsa.pub ~/.ssh/authorized_keys`  

* Second Option How do I add SSH Keys to authorized_keys file?  
`cat ~/.ssh/id_rsa.pub | ssh your_desktop_ssh_user@YOUR.DESKTOP.IP.ADDRESS "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"`  

* Start server in machine that will ssh into  
`sshd`  

* Android remote host into desktop server, assuming default port 8022  
`ssh your_desktop_ssh_user@YOUR.DESKTOP.IP.ADDRESS -p 8022`  

* Desktop remote host into android server, assuming default port 8022  
`ssh your_android_ssh_user@YOUR.ANDROID.IP.ADDRESS`  

* To view the log output from the server process.  
`logcat -s 'syslog:*'`  
