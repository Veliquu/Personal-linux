# Using [the gentoo handboog](https://wiki.gentoo.org/wiki/Handbook:Main_Page) 
Install with openRC
## Useful
### Update config files
Use `dispatch-conf`
### Edit kernel
```bash
$~ cd /usr/src/linux
/usr/src/linux$~ make menuconfig
```
And to recompile the kernel
```bash
$~ make && make modules_install
$~ mount /boot
$~ make install
```

## During installation
### Installing base system
Before running
```bash
$~ emerge --ask --verbose --update --deep --newuse @world
```
I add 2 lines to `/etc/portage/make.conf`  
```bash
ACCEPT_LICENSE="*"
USE="-qtwebengine -webengine"
```
This makes compiling time little faster.  
### Configuring kernel
During installation I use genkernel and I update kernel after installation if I need to change something to make things work.  
### Configuring the bootloader
Install `sys-boot/os-prober` and then add the following line to `/etc/default/grub`  
```bash
GRUB_DISABLE_OS_PROBER=false
```
This is to detect other operating systems from attached drives.  
## After installation  
Add elogind to boot
```bash
$~ rc-update add elogind boot
```
