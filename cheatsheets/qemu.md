#### Keybindings
- Toggle meta/super key focus `Ctrl+alt+g`  

- - -

https://www.spice-space.org/download.html
- - -

#### TTY in a QEMU session
sendkey can be used to send keys to the virtual system that your host intercepts at low level - such as `Ctrl + Alt + F*`.

- Use `Ctrl + Alt + 2` to switch to the QEMU console.
- Type `sendkey ctrl-alt-f1` and press Enter.
- Use `Ctrl + Alt + 1` to switch back to the virtual system, which should now by at TTY1.

Once at a virtual terminal, you should be able to use the chvt command, e.g. `sudo chvt 7` to go back to your X session.
- - -

