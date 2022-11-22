## Copy text from (n)vim to 
```
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
