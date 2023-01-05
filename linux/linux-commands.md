#### Job Control  
* List jobs, job_id is the numerical value of the job  
  `$ jobs`  
* suspend job into background, similar to pause so that one can can do something else  
`<Ctrl-Z>`  
* Can resume it's running in the background by:  
  `$ bg <job_id>`  
* Bring it back to foreground by inserting:  
  `$ fg`  
* Or in case of multiple jobs:  
  `$ fg %<job_id>`  
* To suspend the process running in the background, use:  
  `$ kill -STOP %job_id`  
- - -

#### Copying/Moving/Renaming Files/Directories  
- Shorter syntax to copy/move from/to current file path (current working directory) `$(pwd)`  
NOTE: `.` can also be used but is limited  
  `$ cp -r $(pwd)/path-to/file ~/new/path/`  
  `$ mv -r ~/another/directory/file .`  
- - -

#### Copying/Pasting Text  
- Copy text/output of a command into a file (useful if in putty/non graphical terminal emulator)  
  `$ <command> 2>&1 | tee -a output.txt`  
  or  
  `$ echo "text" 2>&1 | tee -a output.txt` # print text without executing a command  
- - -

#### Recall the Previous Command  
- Use `!!` to express the last command  
  For example if a command needs root permissions:  
  ```bash
  $ touch /opt/file.txt  
  touch: cannot touch '/opt/file.txt': Permission denied  
  $ sudo !!  
  sudo touch /opt/file.txt  
  [sudo] password for user:  
  $ ls -l /opt/myFile.txt  
  -rw-r--r-- 1 root root 0 Dec  21 16:20 /opt/file.txt  
  ```
- - -

#### Getting information about a window  
  - To get id, size, position, state, class, etc...  
  `$ xwininfo`  
  or  
  `$ xdotool getwindowfocus getwindowgeometry` # just get size/position  
- - -

