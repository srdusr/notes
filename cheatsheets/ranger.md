
# Ranger Cheatsheet

## General
Shortcut | Description
---|---
`ranger` | Start Ranger
`Q` | Quit Ranger
`R` | Reload current directory
`?` | Ranger Manpages / Shortcuts


## Movement
Shortcut | Description
---|---
`k` | up
`j` | down
`h` | parent directory
`l`| subdirectory
`gg` | go to top of list
`G` | go t bottom of list
`J` | half page down
`K` | half page up
`H` | History Back
`L` | History Forward
`~` | Switch the view

## File Operations
Shortcut | Description
---|---
`<Enter>` | Open
`r` | open file with
`z` | toggle settings
`o` | change sort order
`zh` | view hidden files
`cw` | rename current file
`yy` | yank / copy
`dd` | cut
`pp` | paste
`/` | search for files `:search`
`n` | next match
`N` | prev match
`<delete>` | Delete


## Commands
Shortcut | Description
---|---
`:` | Execute Range Command
`!` | Execute Shell Command
`chmod` | Change file Permissions
`du` | Disk Usage Current Directory
`S` | Run the terminal in your current ranger window (exit to go back to ranger)

## Tabs
Shortcut | Description
---|---
`C-n` | Create new tab
`C-w` | Close current tab
tab | Next tab
shift + tab | Previous tab
alt + [n] | goto / create [n] tab

## File substituting
Shortcut | Description
---|---
`%f` | Substitute highlighted file
`%d` | Substitute current directory
`%s` | Substitute currently selected files
`%t` | Substitute currently tagged files

### Example for substitution
`:bulkrename %s`

## Marker
Shortcut | Description
---|---
`m  + <letter>` | Create Marker
`um  + <letter>` | Delete Marker
`'  + <letter>` | Go to Marker
`t` | tag a file with an *
`t"<any>` | tag a file with your desired mark

_thx to the comments section for additional shortcuts! post your suggestions there!_




Move around:
up or k ____________ to go up
ctrl-b or pageup ___ to go up a page
ctrl-u or K ________ to go up half page

down or j __________ to go down
ctrl-f or pagedown _ to go down a page
ctrl-d or J ________ to go down half page

left or h __________ to go left
right or l _________ to go right

home _______________ to move to top
end ________________ to move to bottom

H __________________ to history move back
L __________________ to history move forward

ctrl-n or gn _______ to open new tab (in your home)
gc _________________ to close current tab

tab or gt __________ to move to next tab
shift-tab or gT ____ to move to previous tab

cd _________________ to change the working directory to specific directory
gh _________________ to change the working directory to your home
gm _________________ to change the working directory to /media
gM _________________ to change the working directory to /mnt
gu _________________ to change the working directory to /usr

Manage files:
space ______________ to mark a file/directory
v __________________ to mark all files/directories
uv __________________ to unmark all selected files/directories

delete _____________ to delete selected files/directories

yy or f5 ___________ to copy
ya _________________ to add files/directories to current 'copy'
yr _________________ to remove files/directories from current 'copy'

dd or f6 ___________ to cut
da _________________ to add files/directories to current 'cut'
dr _________________ to remove files/directories from current 'cut'

cw _________________ to rename a file/directory
I __________________ to change name of file/directory, from the beginning
A __________________ to change name of file/directory, from the end

/ or f _____________ to search a file/directory
n __________________ to search next file/directory
N __________________ to search previous file/directory

Varies:
q __________________ to quit
s __________________ to launch shell




