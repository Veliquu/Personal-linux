During gentoo installataion use `USE="wayland"` in `/etc/portage/make.conf`  
Add the following line to `/etc/portage/make.cong`:
```bash
ACCEPT_KEYWORDS="~amd64"
```
Whit this you don´t need to be unmasking packages all the time.

# Window Manager
## Screenlock
Installed `swaylock`:
```bash
emerge -av gui-apps/swaylock
```
## Clipboard Manager
Installed `wl-clippoard` to be aplte to copy and paste in the system.
```bash
emerge -av gui-apps/wl-clippoard
```
## Application Launcher 
I instelled `rofi-wayland`
```bash
emerge -av gui-apps/rofi-wayland
```
### Hyprland
In `~/.config/hypr/hyprland.conf` I added exec command to keybind for launching rofi:
```bash
bind = $mainMod, P, exec, rofi -modi run -show run
```
