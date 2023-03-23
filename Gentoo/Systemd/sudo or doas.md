# [SUDO](https://wiki.gentoo.org/wiki/Sudo)
The `sudo` command provides a simple and secure way to configure privilege escalation — i.e., letting normal users execute certain (or even all) commands as `root` or as another user, either with or without giving a password.  
Installing
```bash
root $ emerge --ask app-admin/sudo
```
To configurate go to the folder with following command
```bash
root $ visudo
```
Then uncomment following line in `/etc/sudoers.tmp`
```bash
%wheel ALL=(ALL) ALL
```
Now `wheel` group can make root commands with sudo.  
# [DOAS](https://wiki.gentoo.org/wiki/Doas)
Installing
```bash
root $ emerge --ask app-admin/doas
```
Then add group `wheel` to have root rights.  
So add the following line to `/etc/doas.conf`.
```bash
root $ permit :wheel
```
or  


Using the `persist` keyword `doas` can remember an authenticated user and will not require confirmation by password for a time period of five minutes after the last `doas` command was entered in the terminal window.  
To use `persist` keywoard:
```bash 
root $ echo "app-admin/doas persist" >> /etc/portage/package.use/doas
```
Then recompile the package.  

Then add the following line to `/etc/doas.conf`: 
```bash
permit persist :wheel
```
