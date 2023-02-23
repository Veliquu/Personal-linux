## Installing [xorg](https://wiki.gentoo.org/wiki/Xorg/Guide)
Add `USE="X"` to `/etc/portage/make.conf`.  
Need to also add:
```bash
VIDEO_CARDS=""
INPUT_DEVICES=""
```
To find out what to use, use commands
```bash
portageq envvar VIDEO_CARDS
portageq ennvar INPUT_DEVICES
```
Installing xorg, xorg-drivers and xterm
```bash
$~ emerge -av x11-base/xorg-server x11-base/xorg-drivers
$~ emerge -av x11-terms/xterm
```
After try and see if xorg is working use command `startx`.  
If it works it opens 3 terminal windows and you can exit that from root window and writing `exit`.
