# [Awesome](https://wiki.gentoo.org/wiki/Awesome)

# Prerequisites
## Services
Choose exactly one of:
- elogind: Standalone logind package, extracted from the systemd project for use with OpenRC or other init systems.
- systemd: Uses the session tracker part of systemd. Users of systemd do not need to take any other initiative here.

## Miscellaneous
If `gentoolkit` is not installed, install it with: 
``` bash
root $ emerge -ask gentoolkit
```
### D-bus  
Check if you have D-bus installed:
```bash
root $ equery list "*" | grep dbus
```
If it is not found, then install it with:
```bash
root $ emerge -ask sys-apps/dbus
```
With OpenRC you also need to do following:  
After configuration step, start D-Bus with:
```bash
root $ /etc/init.d/dbus start
```
To start D-Bus at boot time, add it the default run level:
```bash
root $ rc-update add dbus default
```
  
  
### Check if you have polkit installed:
```bash
root $ equery list "*" | grep polkit
```
If not, install it with:
```bash
root $ emerge -ask sys-auth/polkit
```
  
  
### Udisks
Check if you have udisks installed:
```bash
root $ equery list "*" | grep udisk
```
If not, install it with:
```bash
root $ emerge -ask sys-fs/udisks
```
Make sure each user is the plugdev group. Here the example user larry is used.  
```bash
root $ groups larry
wheel audio users plugdev larry
```
f plugdev is not among the available user groups , add user to the plugdev group.
```bash
root $ usermod -a -G plugdev larry
```

## X-server
Follow the guide from [here](https://github.com/Veliquu/Personal-linux/blob/main/Gentoo/Systemd/Desktop%20Enviroment/Xorg.md).  
After that return here.

# Awesome
Installing awesomewm:
```bash
root $ emerge --ask x11-misc/awesome
```
You need to create awesome directoy in your home directory and copy the default configuration file there.
```bash
user $ mkdir -p ~/.config/awesome/
```
```bash
user $ cp /etc/xdg/awesome/rc.lua ~/.config/awesome/rc.lua
```


