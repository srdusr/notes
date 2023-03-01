### SSH (Secure Shell Protocol)  

* Find out your username  
`$ whoami`  

* Check ip address  
** Linux  
`$ ip addr show | grep "inet "`  
`$ ifconfig`  
`$ nmcli -p device show`  
** Windows  
`$ ipconfig`  
> NOTE: The IP Address we use will usually be the one not similar to 127.0.0.1 (localhost) but rather a different string of numbers, ignore any forward slash and the numbers after it  
> Example:  
> `$ ip addr show | grep "inet "`
```bash
> inet 127.0.0.1/8 scope host lo
> inet <u>10.1.1.5</u>/27 brd 10.1.1.31 [...]
```
> The `10.1.1.5` is what we want in this example  

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

2. scp from remote to local using a single file.  
`$ scp remoteuser@remoteserver:/remote/folder/remotefile.txt  localfile.txt`  

* Copy multiple files from remote to local:  
`$ scp your_username@remote.edu:/some/remote/directory/\{a,b,c\} ./`  

* Copy multiple files from local to remote:  

  `$ scp foo.txt bar.txt your_username@remotehost.edu:~`  
  `$ scp {foo,bar}.txt your_username@remotehost.edu:~`  
  `$ scp *.txt your_username@remotehost.edu:~`  

* Copy multiple files from remote to remote:  
  `$ scp your_username@remote1.edu:/some/remote/directory/foobar.txt \`


