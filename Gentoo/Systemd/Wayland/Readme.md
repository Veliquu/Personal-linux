During gentoo installataion use `USE="wayland"` in `/etc/portage/make.conf`

# Window Manager
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
