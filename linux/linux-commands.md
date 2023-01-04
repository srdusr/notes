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
- Copy text/output into a file (useful if in putty/non graphical terminal emulator)  
  `$ <command> 2>&1 | tee output-file`  
  or  
  `$ echo "text" 2>&1 | tee output-file` # print text without executing a command  
- - -
