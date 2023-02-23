# [LightDM](https://wiki.gentoo.org/wiki/LightDM)
Install LightDM:
```bash
root $ emerge --ask x11-misc/lightdm
```
Systemd
To start LightDM on boot:
```bash
root $ systemctl enable lightdm
```
To start LightDM now:
```bash
root $ systemctl start lightdm
```
