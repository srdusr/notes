## Tmux Notes
#### Plugins
* Key bindings for tmux-resurrect  
`<prefix> + Ctrl-s` # save changed to 'W'  
`<prefix> + Ctrl-r` # restore changed to 'E'
* Installing plugins  
`<prefix> + I`  
then reload tmux environment with either:  
$ `tmux source ~/.tmux.conf`  
or if tmux config is in a XDG config base directory  
$ `tmux source ~/.config/tmux/tmux.conf`  
* Plugin uninstall  
Delete or comment out the plugin in .tmux.conf  
Then save and reload
- - -
#### Basic commands/keys
* List keybindings  
$ `tmux list-keys`  
or  
`<prefix>:list-keys`  
or  
`<prefix>:?`  

* Panes Management  
`<prefix>:swap-pane -U` # move current pane up or anti-clockwise  
`<prefix>:swap-pane -D` # move current pane down or clockwise  
`<prefix>{` or `<prefix>(:swap-pane -L)` # move current pane to the left  
`<prefix>}` or `<prefix>(:swap-pane -R)` # move current pane to the right  
`<prefix>q` # show pane numbers (type number to move cursor)  
`<prefix><Space>` # toggle pane arrangements  
`<prefix>Ctrl-o` # rotate window  

* Move cursor to next window  
`<prefix>o`

* Close Window  
`<prefix>&` or `<prefix>:kill-window` # kill window
- - -
#### SESSIONS  
* Start a new session  
$ `tmux`  
$ `tmux new`  
$ `tmux new-session`  
`<prefix>:new`

* Start a new session with the name ***mysession***  
$ `tmux new -s mysession`  
`<prefix>:new -s mysession`

* Kill/delete session mysession  
$ `tmux kill-ses -t mysession`  
$ `tmux kill-session -t mysession`  

* Kill/delete all sessions but the current  
$ `tmux kill-session -a`

* Kill/delete all sessions but mysession  
$ `tmux kill-session -a -t mysession`  

* Rename session  
`<prefix>$`  

* Detach from session  
`<prefix>d`  

* Detach others on the session (Maximize window by detaching other clients)  
`<prefix>:attach -d`  

* Show all sessions  
$ `tmux ls`  
$ `tmux list-sessions`  
`<prefix>s`  

* Attach to last session  
$ `tmux a`  
$ `tmux at`  
$ `tmux attach`  
$ `tmux attach-session`  

* Attach to a session with the name mysession  
$ `tmux a -t mysession`  
$ `tmux at -t mysession`  
$ `tmux attach -t mysession`  
$ `tmux attach-session -t mysession`  

* Move to previous session  
`<prefix>(`  

* Move to next session  
`<prefix>)`  

#### WINDOWS

* Start a new session with the name mysession and window mywindow
$ tmux new -s mysession -n mywindow

* Create window
<prefix> c

* Rename current window
<prefix> ,

* Close current window
<prefix> &

* Previous window
<prefix> p

* Next window
<prefix> n

* Switch/select window by number
<prefix> 0 ... 9

* Reorder window, swap window number 2(src) and 1(dst)
:swap-window -s 2 -t 1

* Move current window to the left by one position
:swap-window -t -1



* PANES

* Toggle last active pane
<prefix> ;

* Split pane horizontally
<prefix> %

* Split pane vertically
<prefix> "

* Move the current pane left
<prefix> {

* Move the current pane right
<prefix> }

* Switch to pane to the direction
<prefix> <Up>
<prefix> <Down>
<prefix> <Right>
<prefix> <Left>

* Toggle synchronize-panes(send command to all panes)
:setw synchronize-panes

* Toggle between pane layouts
<prefix> Spacebar

* Switch to next pane
<prefix> o

* Show pane numbers
<prefix> q

* Switch/select pane by number
<prefix> q 0 ... 9

* Toggle pane zoom
<prefix> z

* Convert pane into a window
<prefix> !

* Resize current pane height(holding second key is optional)
<prefix> + <Up>
<prefix> Ctrl + <Up>
<prefix> + <Down>
<prefix> Ctrl + <Down>

* Resize current pane width(holding second key is optional)
<prefix> + <Up>
<prefix> Ctrl + <Up>
<prefix> + <Down>
<prefix> Ctrl + <Down>

* Close current pane
<prefix> x



* COPY MODE

* Use vi keys in buffer
:setw -g mode-keys vi

* Enter copy mode
<prefix> [

* Enter copy mode and scroll one page up
<prefix> PgUp

* Quit mode
<q>

* Go to top line
<g>

* Go to bottom line
<G>

* Scroll up
<Up>

* Scroll down
<Down>

* Move cursor left
<h>

* Move cursor down
<j>

* Move cursor up
<k>

* Move cursor right
<l>

* Move cursor forward one word at a time
<w>

* Move cursor backward one word at a time
<b>

* Search forward
</>

* Search backward
<?>

* Next keyword occurance
<n>

* Previous keyword occurance
<N>

* Start selection
<Spacebar>

* Clear selection
<Esc>

* Copy selection
<Enter>

* Paste contents of buffer_0
<prefix> ]

* Display buffer_0 contents
:show-buffer

* Copy entire visible contents of pane to a buffer
:capture-pane

* Show all buffers
:list-buffers

* Show all buffers and paste selected
:choose-buffer

* Save buffer contents to buf.txt
:save-buffer buf.txt

* Delete buffer_1
:delete-buffer -b 1



* MISC

* Enter command mode
<prefix> :

* Set OPTION for all sessions
:set -g OPTION

* Set OPTION for all windows
:setw -g OPTION

* Enable mouse mode
:set mouse on



* HELP

* List key bindings(shortcuts)
$ tmux list-keys
:list-keys
<prefix> ?

* Show every session, window, pane, etc...
$ tmux info
