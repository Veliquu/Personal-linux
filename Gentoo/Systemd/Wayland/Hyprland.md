Start installing `eselect/repository`
```bash
emerge --ask app-eselect/eselect-repository
```
  
Next enable `guru` overlay
```bash
eselect repository enable guru
emerge --sync guru
```
You need to unmask the `hyprland` package:
```bash
echo "gui-wm/hyprland **" >> /etc/portage/package.accpet_keywords/hyprland
```
Then install `hyprland`
```bash
emerge --ask --verbose hyprland
```
  
  
## [Launching Hyprland](https://wiki.hyprland.org/0.22.0beta/Getting-Started/Master-Tutorial/)
Make an executable file somewhere in your PATH, for example ~/.local/bin/, called (for example) wrappedhl.  

In it, put:
```bash
#!/bin/sh

cd ~

# Log WLR errors and logs to the hyprland log. Recommended
export HYPRLAND_LOG_WLR=1

# Tell XWayland to use a cursor theme
export XCURSOR_THEME=Bibata-Modern-Classic

# Set a cursor size
export XCURSOR_SIZE=24

# Example IME Support: fcitx
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
export SDL_IM_MODULE=fcitx
export GLFW_IM_MODULE=ibus

exec Hyprland
```
Mke the file executable:
```bash
chmod 744 ~/.local/bin/wrappedhl
```
Afetr that I created alias for executing the script in `.bashrc`:
```bash
alias hypr=´~/.local/bin/wrappedhl´
```
## Monitor
Next unmask and install `wlr-randr` to get your monitor information:
```bash
echo "gui-apps/wlr-randr **" >> /etc/portage/package.accpet_keywords/wlr-randr
emerge -av wlr-randr
```
