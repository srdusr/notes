# zathura
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
OPTIONS
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

-e,--reparent=xid

Reparents to window specified by xid

-c,--config-dir=path

Path to the config directory

-d,--data-dir=path

Path to the data directory

-p,--plugins-dir=path

Path to the directory containing plugins

-w,--password=password

The documents password. If multiple documents are opened at once, the password will be used for the first one and zathura will ask for the passwords of the remaining files if needed.

-P,--page=number

Opens the document at the given page number. Pages are numbered starting with 1, and negative numbers indicate page numbers starting from the end of the document, -1 being the last page.

-f,--find=string

Opens the document and searches for the given string.

-l,--log-level=level

Set log level (debug, info, warning, error)

-x,--synctex-editor-command=command

Set the synctex editor command. Overrides the synctex-editor-command setting.

--synctex-forward=input

Jump to the given position. The switch expects the same format as specified for synctex's view -i. If no instance is running for the specified document, a new instance will be launched (only if --synctex-pid is not specified).

--synctex-pid=pid

Instead of looking for an instance having the correct file opened, try only the instance with the given PID. Note that if the given PID does not have the correct file open or does not exist, no new instance will be spanned.

--mode=mode

Start in a non-default mode


--fork


Fork into background


--version

Display version string and exit


--help


Display help and exit

""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
MOUSE AND KEY BINDINGS
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

General
--------

J, PgDn

Go to the next page

K, PgUp

Go to the previous page

h, k, j, l

Scroll to the left, down, up or right direction

Left, Down, Up, Right

Scroll to the left, down, up or right direction

^t, ^d, ^u, ^y

Scroll a half page left, down, up or right

t, ^f, ^b, space, <S-space>, y

Scroll a full page left, down, up or right

gg, G, nG

Goto to the first, the last or to the nth page


P


Snaps to the current page


H, L


Goto top or bottom of the current page


^o, ^i


Move backward and forward through the jump list


^j, ^k


Bisect forward and backward between the last two jump points

^c, Escape

Abort


a, s


Adjust window in best-fit or width mode



/, ?


Search for text



n, N


Search for the next or previous result



o, O


Open document



f


Follow links



F


Display link target



c


Copy link target into the clipboard



:


Enter command



r


Rotate by 90 degrees



^r


Recolor (grayscale and invert colors)



R


Reload document



Tab


Show index and switch to Index mode



d


Toggle dual page view



F5


Switch to presentation mode



F11


Switch to fullscreen mode



^m


Toggle inputbar



^n


Toggle statusbar


+, -, =

Zoom in, out or to the original size

zI, zO, z0

Zoom in, out or to the original size


n=


Zoom to size n



mX


Set a quickmark to a letter or number X



'X


Goto quickmark saved at letter or number X



q


Quit


Fullscreen mode


J, K


Go to the next or previous page


space, <S-space>, <BackSpace>

Scroll a full page down or up

gg, G, nG

Goto to the first, the last or to the nth page

^c, Escape

Abort


F11


Switch to normal mode


+, -, =

Zoom in, out or to the original size

zI, zO, z0

Zoom in, out or to the original size


n=


Zoom to size n



q


Quit


Presentation mode

space, <S-space>, <BackSpace>

Scroll a full page down or up

^c, Escape

Abort


F5


Switch to normal mode



q


Quit


Index mode


k, j


Move to upper or lower entry



l


Expand entry



L


Expand all entries



h


Collapse entry



H


Collapse all entries


space, Return

Select and open entry

Mouse bindings


Scroll


Scroll up or down


^Scroll

Zoom in or out

Hold Button2

Pan the document

Button1

Follow link

"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
COMMANDS
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

bmark


Save a bookmark


bdelete

Delete a bookmark


blist


List bookmarks



close


Close document



exec


Execute an external command



info


Show document information



open


Open a document



offset


Set page offset



print


Print document


write(!)

Save document (and force overwriting)


export


Export attachments


dump


Write values, descriptions, etc. of all current settings to a file.
