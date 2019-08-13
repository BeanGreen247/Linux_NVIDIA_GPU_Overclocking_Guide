# Linux NVIDIA GPU overclocking Guide
## The Guide Part 1
First enable cool-bits
```
sudo nvidia-xconfig -a --cool-bits=28
```
Next we will edit the xorg config file
```
sudo nano /etc/X11/xorg.conf
```
Scroll down till you find Section "Screen"
```
Section "Screen"
    Identifier     "Screen0"
    Device         "Device0"
    Monitor        "Monitor0"
    DefaultDepth    24
    Option         "Coolbits" "28"
    SubSection     "Display"
        Depth       24
    EndSubSection
EndSection
```
Add this line under [Option         "Coolbits" "28"]
```
Option         "RegistryDwords" "PowerMizerEnable=0x1; PerfLevelSrc=0x2222; PowerMizerDefaultAC=0x1"
```
So it looks like this 
```
Section "ScreeSection "Screen"
    Identifier     "Screen0"SectioSection "Screen"
    Identifier     "Screen0"
    Device         "Device0"
    Monitor        "Monitor0"
    DefaultDepth    24
    Option         "Coolbits" "28"
    Option         "RegistryDwords" "PowerMizerEnable=0x1; PerfLevelSrc=0x2222; PowerMizerDefaultAC=0x1"
    SubSection     "Display"
        Depth       24
    EndSubSection
EndSection
```
Once done reboot.

## The Guide Part 2

Next lets create a overclocking script to overclock our gpu automatically

The number "#1" has to be the same and number "#" can be any number. Make sure those numbers match in the NVIDIA X Server Settings.
```
sudo nano /usr/bin/overclock.sh
!/bin/bash
nvidia-settings -a '[gpu:0]/GPUGraphicsClockOffset[1]=#'

nvidia-settings -a '[gpu:0]/GPUGraphicsMemoryOffset[1]=#1'

nvidia-settings -a '[gpu:0]/GPUMemoryTransferRateOffset[1]=#1'

nvidia-settings -a '[gpu:0]/GPUFanControlState=#'

nvidia-settings -a '[fan:0]/GPUTargetFanSpeed=#'
```
Next make it executable
```
sudo chmod +x /usr/bin/overclock.sh
```
And add it to startup for XFCE its in Application>Settings>Settings Manager>Session and Startup>Application Autostart
Then click on Add. Give it a name, desciption and in command type the location /usr/bin/overclock.sh.
```
/usr/bin/overclock.sh
```
That will automatically overclock your GPU at startup.

To make sure it works reboot for the last and final time and enjoy your overclocked GPU.
