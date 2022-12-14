
#### Vim Keyboard Shortcuts

* Movement
```
h        -   Move left
j        -   Move down
k        -   Move up
l        -   Move right
$        -   Move to end of line
0        -   Move to beginning of line (including whitespace)
^        -   Move to first character on line
gg       -   Move to first line of file
G        -   Move to last line of file

w        -   Move forward to next word, with cursor on first character (use W to jump by whitespace only)
b        -   Move backward to next word, with cursor on first character (use B to jump by whitespace only)
e        -   Move forward to next word, with cursor on last character (use E to jump by whitespace only)
ge       -   Move backwards to next word, with cursor on last character (use gE to jump by whitespace only)
(        -   Move to beginning of previous sentence. Use ) to go to next sentence
{        -   Move to beginning of previous paragraph. Use } to go to next paragraph
+        -   Move forward to the first character on the next line
-        -   Move backwards to the first character on the previous line

CTRL+u   -   Move up by half a page
CTRL+d   -   Move down by half a page
CTRL+b   -   Move up by a page
CTRL+f   -   Move down by a page

H        -   Move cursor to header (top) line of current visible window
M        -   Move cursor to middle line of current visible window
L        -   Move cursor to last line of current visible window

fc       -   Move cursor to next occurrence of character c on the current line. Use Fc to move backwards
tc       -   Move cursor till next character c on the current line. Use Tc to move backwards
%        -   Move cursor to next brace, bracket or comment paired to the current cursor location

*        -   Search forward for word under cursor
#        -   Search backwards for word under cursor
/word    -   Search forward for word. Accepts regular expressions to search
?word    -   Search backwards for word. Accepts regular expressions to search
n        -   Repeat the last / or ? command
N        -   Repeat the last / or ? command in the opposite direction
```

* NORMAL MODE -> INSERT MODE
```
i        -   Enter insert mode to the left of the cursor
a        -   Enter insert mode to the right of the cursor
I        -   Enter insert mode at first character of current line
A        -   Enter insert mode at last character of current line

o        -   Insert line below current line and enter insert mode
O        -   Insert line above current line and enter insert mode

cm       -   Delete (change) the character or word (w) in motion m, then enter insert mode
cc       -   Delete current line and enter insert mode (unlike dd which leaves you in normal mode)
C        -   Delete (change) from cursor to end of line, and enter insert mode
```
* VISUAL MODE
```
v        -   Enter visual mode and highlight characters
V        -   Enter visual mode and highlight lines
CTRL+v   -   Enter visual block mode and highlight exactly where the cursor moves
o        -   Switch cursor from first & last character of highlighted block while in visual mode
~        -   Swap case under selection
<<       -   Shift lines to left
>>       -   Shift lines to right

vat      -   Highlight all text up to and including the parent element
vit      -   Highlight all text up to the parent element, excluding the element
vac      -   Highlight all text including the pair marked with c (like va<, va' or va")
vic      -   Highlight all text inside the pair marked with c
```

* Deletion
```
x        -   Delete character forward (under cursor). use x do delete backwards (before cursor)
r        -   Replace single character under cursor, and remain in normal mode
s        -   Delete character under cursor, then switch to insert mode

dm       -   Delete in direction of movement m. For m, you can also use w, b, or any other variation
dd       -   Delete entire current line
D        -   Delete until end of line
```

* Yank & Put
```
y        -   Yank (copy) highlighted text
yy       -   Yank current linepPut (paste) yanked text below current line
yw       -   Yank a word from the cursor
ynw      -   Yank n words from the cursor
y$       -   Yank till the end of the line
P        -   Put yanked text above current line
J        -   Join current line with the next line. Use gJ to exclude join-position space
xp       -   Transpose two letters (delete and paste, technically)
```

* Marking
```
ma        -   Set a marker a at cursor position to come back to later. a can be any character you choose
mb        -   Set a marker b at current position
`a        -   Move cursor to exact position of the marker you set with ma
'a        -   Move cursor to the first character of the line marked with ma

d'a       -   Delete from current line to line of mark a
d`a       -   Delete from current cursor position to position of mark a
c'a       -   Change text from current line to line of mark a
y`a       -   Yank text to unnamed buffer from cursor to position of mark a

:marks 	  -   List all the current marks
:marks ab -   List marks a, b

'a,'bs/test/foo/g - Search and replace test with foo between markers a and b

```

* Vim Folding
```
zf#j      -   creates a fold from the cursor down # lines.
zf/string -   creates a fold from the cursor to string .
v{move}zf -   creates a visual select fold
zf'a      -   creates a fold from cursor to mark a

zo        -   opens a fold at the cursor.
zO        -   opens all folds at the cursor.
za        -   Toggles a fold at the cursor.
zc        -   closes a fold at the cursor.
zM        -   closes all open folds.
zd        -   deletes the fold at the cursor.
zE        -   deletes all folds.

zj        -   moves the cursor to the next fold.
zk        -   moves the cursor to the previous fold.
zm        -   increases the foldlevel by one.
zr        -   decreases the foldlevel by one.
zR        -   decreases the foldlevel to zero -- all folds will be open.
[z        -   move to start of open fold.
]z        -   move to end of open fold.

:set foldmethod=manual         -  default method v{select block}zf to fold
:set foldmethod=marker         -  use marker fold method {{{
:set foldemethod=marker/*,*/   -  user custom marker fold method
:set foldmethod=indent         -  automatically fold programms per its indentation
```

* Miscellaneous
```
u        -   Undo
U        -   Undo all changes on current line
CTRL+R   -   Redo
.        -   Redo

g~       -   switch case under cursor
g~$      -   Toggle case of all characters to end of line.
g~~      -   Toggle case of the current line (same as V~).
gUU      -   switch the current line to upper case
guu      -   switch the current line to lower case

CTRL+A   -   Increment the number at cursor
CTRL+X   -   Decrement the number at cursor

.        -   Repeat last change or delete
;        -   Repeat last f, t, F, or T command
,        -   Repeat last f, t, F, or T command in opposite direction
```
- - -
#### Buffers
```
:ls (or :buffers)   -   list / show available buffers
:e filename         -   Edit a file in a new buffer
:bnext (or :bn)     -   go to next buffer
:bprev (of :bp)     -   go to previous buffer
:bdelete (or :bd)   -   unload a buffer (close a file)
:bwipeout (or :bw)  -   unload a buffer and deletes it
:b [N]              -   The number of the buffer you are interested to open
:ball               -   opens up all available buffers in horizontal split window
:vertical ball      -   opens up all available buffero in vertical split window
:q                  -   close the buffer window
:help buffers       -   help for buffers
:r <file_path>      -   reads a file from the path to the buffer
:r !<command>       -   reads the output of the command into buffer
:.! cat <file_path> -   reads the output of the command (eg: cat) into buffer or !! in ex-mode
```
- - -
#### Windows

* Window management
```
*split screen horizontal
:split filename
vim -o file1 file2

*split screen vertical
:vs filename
or
:vsplit filename
vim -O file1 file2

*close current window
:hide

*Horizontal resize in active window
:resize 20

*vertical resize
:vertical resize 20

*diff
:windo diffthis -  diff between 2 vsplit windows
:diffs, diffsplit {filename} - diffs the current window with the file given
:diffoff  - turns off diff selection

CTRL+w s       -   Split current window horizontally
CTRL+w v       -   Split current window vertically
CTRL+w c       -   Close current window
CTRL+w m       -   Move to window according to motion m
CTRL+w o       -   Maxmize current window (note: this overwrites your current window configuration)

* EX Mode
:Vex           - Open Vertical Split in ex mode with file browser
:Sex           - Open Vertical Split in ex mode with file browser

```

* Moving windows
```
CTRL+W r       -   Swap bottom/top if split horizontally
CTRL+W R       -   Swap top/bottom if split horizontally

CTRL+w r       -   Rotates the windows from left to right - only if the windows are split vertically
CTRL+w R       -   Rotates the windows from right to left - only if the windows are split vertically

CTRL+w H       -   Move current window the far left and use the full height of the screen
CTRL+w J       -   Move current window the far bottom and use the full width of the screen
CTRL+w K       -   Move current window the far top and full width of the screen
CTRL+w L       -   Move current window the far right and full height of the screen
```

* Navigate between windows
```
CTRL+w CTRL+w  -   switch between windows
CTRL+w UP      -   Move to the top window from current window
CTRL+w DOWN    -   Move to the bottom window from current window
CTRL+w LEFT    -   Move to the left window from current window
CTRL+w RIGHT   -   Move to the right window from current window
```

* Resizing windows
```
*Sometimes windows open up funny or are rendered incorrectly after separating from an external monitor. Or maybe you want to make more room for an important file.

CTRL+w _       -   Max out the height of the current split
CTRL+w |       -   Max out the width of the current split
CTRL+w =       -   Normalize all split sizes, which is very handy when resizing terminal

CTRL+w >       -   Incrementally increase the window to the right. Takes a parameter, e.g. CTRL-w 20 >
CTRL+w <       -   Incrementally increase the window to the left. Takes a parameter, e.g. CTRL-w 20 <
CTRL+w -       -   Incrementally decrease the window's height. Takes a parameter, e.g. CTRL-w 10 -
CTRL+w +       -   Incrementally increase the window's height. Takes a parameter, e.g. CTRL-w 10 +
```
- - -
#### Tabs
```
:tabe filename      -   opens the file in newtab
:tabe new           -   open an empty tab
:tabs               -   list opened tabs
:tabc               -   close the active tab
:tabn and tabp      -   Go to next tab or previous tab
:tabfirst           -   Go to the first available tab
:tablast            -   Go to the last available tab
:help tabpage       -   help for tabs

vim -p *.txt        -   open all txt files in tabs
```

* Tab navigation
```
gt                  -   go to next tab
gT                  -   go to previous tab
{i}gt               -   go to tab in position i
```

* Tab shortcuts
```
CTRL+W T            -   Break out current window into a new tabview
CTRL+W o            -   Close every window in the current tabview but the current one
CTRL+W n            -   create a new window in the current tabview
CTRL+W c            -   Close current window in the current tabview
```
- - -

#### Search & Replace

The `:substitute` command searches for a text pattern, and replaces it with a text string. There are many options, but these are probably what we want:  
* Find each occurrence of 'foo' (in the current line only), and replace it with 'bar'  
    \: `s/foo/bar/g`  
* Find each occurrence of 'foo' (in all lines), and replace it with 'bar'  
    \: `%s/foo/bar/g`  
* Change each 'foo' to 'bar', but ask for confirmation first  
    \: `%s/foo/bar/gc`  
* Change only whole words exactly matching 'foo' to 'bar'; ask for confirmation  
    \: `%s/\<foo\>/bar/gc`  
* Change each 'foo' (case insensitive due to the i flag) to 'bar'; ask for confirmation  
    \: `%s/foo/bar/gci`  
* This may be wanted after using :set noignorecase to make searches case sensitive (the default)  
    \: `%s/foo\c/bar/gc` is the same because \c makes the search case insensitive.
* Change each 'foo' (case sensitive due to the I flag) to 'bar'; ask for confirmation  
    \: `%s/foo/bar/gcI`  
- - -

* Permission override
```
:w !sudo tee %            -    Allows to override the permission of the written file
:w !sudo sh -c "cat > %"  -             "                            "

```

* Create a new file named filename in the same directory as the currently open file, and write it.  
    \: `e %:h/filename`  

* Copy text from (n)vim to other applications
```bash
* linux:
  :w !xclip -sel c # copy the whole file
  $ xclip -o sel -c # paste from the clipboard
or 
  :w !xsel -b # copy the whole file
  $ xsel -o -b # paste from the clipboard
-- Note: In case neither of these tools (xsel and xclip) are preinstalled on your distro, you can probably find them in the repos
* macos:
  :%w !pbcopy # copy the whole file 
  :r !pbpaste # paste from the clipboard 
```

* To open the current window in a new tab (maximize) with the cursor in the same place, enter  
    \: `tab sp` # splits the current window into a new tab  
     or  
    `<Ctrl-w>T`  
* To close the current window, press  
    `<Ctrl-w>c`  

* To make a file executable  
    \: `! chmod +x %`  

* Shortcut command to backup current file  
    \: `!cp % %.backup`  

* Use hjkl... at vim's command history mode by using `<C-f>` or immediatly go
  into history mode `q:` and exit by pressing `<enter>`

* Split existing buffer into a horizontal/vertical window  
    \: `sb` # horizontal  
    \: `vert sb` # vertical  
    \: `sb<n>` # where n is a specific buffer number
- - -


vim +10 <file_name>            - opens the file at line 10
vim +/bash cronjob-lab.yml     - opens the file cronjob-lab.yml on the first occurence of bash

vim scp://balasundaramm@mgmt-bst:22/~/automation/test-file.txt - Edit a remote file via scp

gg=G            -   Format HTML. Make sure FileType is set to html with :setf html
CTRL+n          -   Press after typing part of a word. It scrolls down the list of all previously used words
CTRL+p          -   Press after typing part of a word. It scrolls up the list of all previously used words

