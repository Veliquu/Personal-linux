# Using [the gentoo handboog](https://wiki.gentoo.org/wiki/Handbook:Main_Page) 
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
## After installation  
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
$~ wpa_supplicant 'SSID' 'password' >> /etc/wpa_supplicant/wpa_supplicant-[wifi card].conf
```
You can remove the line showing your password as it is commented out.  
It helps security to not have file including your wifi password.  
Lastly we want to initialise wpa_supplicant with the information we have given in to the config file.
```bash
wpa_supplicant -B -i [wifi card] -c /etc/wpa_supplicant/wpa_supplicant-[wifi card].conf
```
