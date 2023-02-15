# Lenovo touchpad kernel configuration
## If nonly gestures not working, it is usually missing this:
```bash
Device Drivers --- >
    HID support --- >
        Special HID drivers --- >
            < * > HID multitouch panels
```
## If it is not recognized, a configuration is usually missing in the kernel. What (almost) is always neede:  
1) Low Power System (Notebook)
2) i2c
3) gpio
4) pinctrl
5) hid support
6) input

These differ between a) INTEL and b) AMD systems:  
### 1a) Intel Low Power System
```bash
Processor type and features --- >
    [ * ] Intel Low Power Subsystem Support

Device Drivers --- >
    Multifunction device drivers --- >
        [ * ] Intel I LPC
        [ * ] Intel Low Power Subsystem support in PCI mode
        [ * ] Intel Low Power Subsystem support in ACPI mode
```
### 1b) AMD Low Power System
```bash
Processor type and features --- >
    [ * ] AMD ACPI2Platform devices support
```
  
### 2) See: [https://wiki.gentoo.org/wiki/I2C](https//wiki.gentoo.org/wiki/I2C)  
Intel systems almost always only need the Intel 82801; see: [https://www.kernel.org/doc/html/latest/i2c/busses/i2c-i801.html](https://www.kernel.org/doc/html/latest/i2c/busses/i2c-i801.html)  
Choose for Synopsys under these modules:
```bash
Device Drivers --- >
    I2C support --- >
        i2C Hardware Bus support --- >
            [? ] AMD 8111
            [? ] AMD MP2 PCIe
            [? ] Intel 82801 ( ICH / PCH )
            [? ] SMBus Control Method Interface
            [? ] Synopsys DesignWare Platform
            [? ] Synopsys DesignWare PCI
```
### 3a) Intel gpio (in order for this to be selected, the "Intel I LPC" must have been enabled beforhand in 1a; otherwise you don't see it at all)  
```bash
Device Drivers --- >
    [ * ] GPIO Support --- >
        [ * ] Character device ( / dev / gpiochipN ) support
        Memory mapped GPIO drivers --- >
            [ * ] Intel I GPIO
```
### 3b) AMD gpio. Most of the time, the following ( 4b ) is sufficient and nothing has to be done here unless you really have a very special part. So look in your list.  
```bash
Device Drivers --- >
    [ * ] GPIO Support --- >
        [ * ] Character device ( / dev / gpiochipN ) support
        Memory mapped GPIO drivers --- >
            ( see your output of "lsmod" )
```
### 4a) Intel pinctrl. Search here for the code name of your CPU and the code name of the chipset, or. Platform Controller Hubs ( PCH ):  
[https://en.wikipedia.org/wiki/List_of_Intel_microprocessors](https://en.wikipedia.org/wiki/List_of_Intel_microprocessors)  
[https://en.wikipedia.org/wiki/Platform_Controller_Hub](https://en.wikipedia.org/wiki/Platform_Controller_Hub)  
[https://en.wikipedia.org/wiki/List_of_Intel_chipsets](https://en.wikipedia.org/wiki/List_of_Intel_chipsets)  
These code names are used in the following section. If none of your code names is included, use an older one because some are upward compatible and are used for several generations. ( Example: My Intel i7-6700 is a "Skylake" on a Gigabyte Z270 mainboard, meaning "Union Point". However, this menu item does not exist because the older PCH is compatible. That's why I use the "Sunrise Point". )  
```bash
Device Drivers --- >
    Pin controllers --- >
        One of these Intel Modules; see codenames
```
### 4b) AMD pinctrl
```bash
Device Drivers --- >
    Pin controllers --- >
        [ * ] AMD GPIO pin control
```
Even if I don't understand it, but it was ( sometimes? ) necessary to configure pinctrl statically < *>, instead of < M > odul !

### 5) hid support
```bash
Device Drivers --- >
    HID support --- >
        [ * ] / dev / hidraw raw HID device support
        [ * ] Generic HID driver
        I2C HID support --- >
            [ * ] HID over I2C transport layer
```
### 6) input. For most touchpads, the "Event interface" ( is sufficient, which we already have enabled; see "Libinput" ). For an i2c-ELAN touchpad, add all of these modules:  
```bash
Device Drivers --- >
    Input device support --- >
        Mice --- >
            [ * ] ELAN I2C Touchpad support
            [ * ] Enable I2C support
            [ * ] Enable SMbus support
```
If your notebook has one Synopsis design goods PCIe controller it may be necessary to activate the following:  
```bash
Device Drivers --- >
    [ * ] PCI support --- >
        PCI controller drivers --- >
            DesignWare PCI Core Support --- >
                [ * ] Platform bus based DesignWare PCIe Controller - Host mode
```
---

Source: [https://forums.gentoo.org/viewtopic-p-8692426.html#8692426](https://forums.gentoo.org/viewtopic-p-8692426.html#8692426)
