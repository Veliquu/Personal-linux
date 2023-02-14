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
### Wifi working
Get your wifi card with `ifconfig`  
Making wifi working after installation I created file:  
```bash
$~ touch /etc/wpa_supplicant/wpa_supplicant-[wifi card].conf
```
Then nano to that file and add there:
```bash
ctrl_interface=/run/wpa_supplicant
update_config=1
```
After that we use `wpa_passphrase` to get your wifi info to the config file
```bash
$~ wpa_passphrase 'SSID' 'password' >> /etc/wpa_supplicant/wpa_supplicant-[wifi card].conf
```
You can remove the line showing your password as it is commented out.  
It helps security to not have file including your wifi password.  
Lastly we want to initialise wpa_supplicant with the information we have given in to the config file.
```bash
wpa_supplicant -B -i [wifi card] -c /etc/wpa_supplicant/wpa_supplicant-[wifi card].conf
```
### Install sudo
```bash
emerge -av app-admin/sudo
``` 
Uncomment `%wheel ALL=(ALL:ALL) ALL` in `/etc/sudoers` to give sudo permissions to everyone in group wheel.  
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

### Installing qtile
Install dmenu alongside qtile
```bash
emerge -av x11-wm/qtile x11-misc/dmenu
```


