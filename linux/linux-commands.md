## Job Control
* List jobs, job_id is the numerical value of the job
$ jobs
* suspend job into background, similar to pause so that one can can do something else
<Ctrl-Z>
* Can resume it's running in the background by:
$ bg <job_id>
* Bring it back to foreground by inserting:
$ fg
* Or this incase of multiple jobs:
$ fg %<job_id>
* To suspend the process running in the background, use:
$ kill -STOP %job_id

## Copy text/output into a file (useful if in putty/non graphical terminal emulator)
$ <command> 2>&1 | tee output-file
