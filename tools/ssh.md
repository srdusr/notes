### SSH (Secure Shell Protocol)  
- A method for secure remote login from one computer to another
> \# Add information about local and target to define which machines

* Find out your username  
`$ whoami`  

* Check ip address  
> NOTE:  
    - lo usually stands for the loopback interface (localhost)  
    - wlan usually stands for a wireless networking interface  
    - rmnet interfaces are usually associated with cellular connections and usb tethering  
  * Linux  
`$ ip addr show | grep "inet "`  
`$ ifconfig`  
`$ nmcli -p device show`  
`$ ip route get 1.2.3.4 | awk '{print $7}'`  
`$ curl ifconfig.me`  
`$ ifconfig 2> /dev/null | grep -Eo 'inet (addr:)?([0-9]*\.){3}[0-9]*' | grep -Eo '[0-9.]*'`


  * Windows  
`$ ipconfig`  
> NOTE: The IP Address we use will usually be the one not similar to 127.0.0.1 (localhost) but rather a different string of numbers, ignore any forward slash and the numbers after it  
> Example:  
> `$ ip addr show | grep "inet "`
```bash
 inet 127.0.0.1/8 scope host lo  
 inet <u>10.1.1.5</u>/27 brd 10.1.1.31 [...]  
```
> The `10.1.1.5` is what we want in this example  

* See if any current ssh is running  
`$ ps aux | grep sshd`  

* Terminate sshd
- See all sshd connections, if non-zero number then there are ssh processes running  
`$ pgrep -c sshd`  
`$ pkill --signal HUP sshd`  
- Check connections again to make sure, if still not 0 then use this  
`$ pkill --signal KILL`  

* Disconnect specific ssh clients off from server  
1. First see who's logged into the the machine  
`$ who` or `$ w`# if there is anything besides tty1, example `pts/3` then there is an active connection 
> NOTE will not work for Termux since it does not support `utmp / wtmp / btmp` files
2. Look for specific process ID `PID`
`$ ps t`  
3. (Optional) Laugh at their impending disconnection
`$ echo "HAHAHAHAHAHAHAHA" | write <user> pts/<n>`
4. Kill the process
`$ kill -9 30737`  



* If `sshd` on remote server produces the following error message: `sshd re-exec requires execution with an absolute path` then use this `/usr/sbin/sshd`  
* If `sshd` on remote server produces the following error message: `sshd: no hostkeys available -- exiting` then use this `ssh-keygen -A`

* For Termux users:
> NOTE: ip addr will not work unless phone is rooted, but `ifconfig` will from `net-tools` since the `proc_net` and `proc_net_tcp_udp` files are not accessible to `untrusted_app` domain but are allowed for `shell` (`adb`).
* Termux install openssh  
`$ pkg in openssh`  

* Termux make sure user/root password is set  
`$ passwd <user> # root does not need to be specified`  

* Generate your ssh key pair on remote host machine, not on server machine  
`$ ssh-keygen`  

* Accessing termux user environment from other consoles  
`$ scp your_desktop_ssh_user@YOUR.DESKTOP.IP.ADDRESS:~/.ssh/id_rsa.pub ~/.ssh/authorized_keys`  

* Second Option How do I add SSH Keys to authorized_keys file?  
`$ cat ~/.ssh/id_rsa.pub | ssh your_desktop_ssh_user@YOUR.DESKTOP.IP.ADDRESS "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"`  

* Start server in machine that will ssh into  
`$ sshd`  


* Android remote host into desktop server, assuming default port 8022  
`$ ssh your_desktop_ssh_user@YOUR.DESKTOP.IP.ADDRESS -p 8022`  

* Desktop remote host into android server, assuming default port 8022  
`$ ssh your_android_ssh_user@YOUR.ANDROID.IP.ADDRESS`  

* To view the log output from the server process.  
`$ logcat -s 'syslog:*'`  


#### Copying files  
##### (SCP Secure Copy Protocol)  
- Syntax:  
```bash
scp [OPTIONS] [[user@]src_host:]file1 [[user@]dest_host:]file2
```
```bash
scp file <remote_username>@<IPorHost>:<PathToFile>   <LocalFileLocation>
```

How to SSH File Transfer from Remote to Local
1. Copy single file from local to remote using scp.  
`$ scp myfile.txt remoteuser@remoteserver:/remote/folder/`  

2. scp from remote to local on local using a single file.  
`$ scp -P 22 remoteserver:/remote/folder/remotefile ~/localdir/localfile`  

* Copy multiple files from remote to local on locall:  
`$ scp your_username@remote.edu:/some/remote/directory/\{a,b,c\} ./`  

* Copy multiple files from local to remote:  

  `$ scp foo.txt bar.txt your_username@remotehost.edu:~`  
  `$ scp {foo,bar}.txt your_username@remotehost.edu:~`  
  `$ scp *.txt your_username@remotehost.edu:~`  

* Copy multiple files from remote to remote:  
  `$ scp your_username@remote1.edu:/some/remote/directory/foobar.txt \`

3. Move 'r' using scp from remote to local on local using a single file.  
`$ scp -r -P 22 remoteserver:/remote/folder/remotefile ~/localdir/localfile`  

- - -

- (Optional) Install openssh
`$ apt install openssh`

- Make sure `passwd` is set for the remote/local machine (root/non-root user)  
`# passwd` # For root  
or  
`$ passwd <username>` # For user  

- Confirm that machines are connected to the internet/LAN or via cables if possible
- Get the IP address (recommended to get both remote and local)  
`# ip a`  
or  
`# ifconfig`  
> NOTE: Getting the correct IP address will vary in method and might require trial and error.  
A few factors to consider are whether either remote/local are in a VM and what OS is being used, example Windows would use `# ipconfig`.  
- If the remote machine is root then confirm that `PermitRootLogin yes` is set in /etc/ssh/sshd_config on the remote machine. If it's not, set it  
`# vim /etc/ssh/sshd_config`  
> NOTE: - Optional find and change the default line `#Port 22` to desired port, example: `Port 8022`  
- Reload the sshd daemon on the remote machine  
`# pkill sshd && /usr/bin/sshd`  
- Generate keys  
`# ssh-keygen A`  
`# ssh-keygen`  
 or  
 `$ ssh-keygen -b 4096 -t rsa`  
> NOTE: No need to enter passphrase unless desired.  
- OpenSSH has a utility to send the key remotely to either machine, only use the `-p` flag if specifying a `<port>` to use 
`$ ssh-copy-id -p <port> -i ~/.ssh/id_rsa.pub user@ip.address`  
> NOTE: Working out which `<port>` to use (default is usually 22) might also require trial and error dependent on remote/local configurations. Some commands to check current active ports: `lsof -Pi | grep ssh` and `netstat -lntu`.
- Connect to the target machine on the local machine via ssh  
`# ssh -p <port> root@ip.address`  
- On server machine edit sshd_config
`$ vi /etc/ssh/sshd_config`


- - -

#### Trouble-shooting
- Check or disable firewall
`$ sudo ufw status`
`$ sudo ufw disable`
`$ sudo ufw reload`
`$ sudo ufw allow port/tcp` # if default port 22
`$ sudo ufw allow 8022/tcp` # if using specific port

