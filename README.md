# CreatorBot-3D-Pro-Series-II-Installing-OctoPi
OctoPi, OctoDash, Touch Drivers, etc.

# Introduction

Since this printer comes with a touch screen, you might aswell have a GUI on it. OctoDash gives you access to key controls right from the touch screen

1. Update the system: `sudo apt update`
2. Upgrade packages; `sudo apt upgrade`
3. Enable Auto-login console in `raspi-config`
4. Reboot: `sudo reboot`
5. Use the script below to Install OctoDash

This script is also on the OctoDash Github
```
bash <(wget -qO- https://github.com/UnchartedBull/OctoDash/raw/main/scripts/install.sh)
```

6. Follow the selection prompts. *The last prompt will reboot the Pi*

[OctoDash Github](https://github.com/UnchartedBull/OctoDash)

[@ChrisRiley Installation Video](https://m.youtube.com/watch?v=kwo3HMBnqC4)

# Touch Driver Install

The screen is a genwric HDMI resistove/capacitive touch display that is connected via SPI.

1. `sudo raspi-config` -> Interface Options -> SPI -> Enable -> Reboot
2. Enter the config file `sudo nano /boot/firmware/config.txt`
3. Add the following to the bottom of the file: 
   
``` dtoverlay=ads7846,cs=1,penirq=25,penirq_pull=2,speed=50000,keep_vref_on=0,swapxy=0,pmax=255,xohms=150,xmin=200,xmax=3900,ymin=200,ymax=3900
```

4. Save (`Ctrl+O`, `Enter`) and exit (`Ctrl+X`), then reboot

# OctoDash Setup

- **Feed Length**: 80-120mm
- **Feed Speed**: 3-5mm/s
*If it stops short of extruding at the nozzle, increase length; if it grinds/skips, decrease speed*
- **API Key**: Click the verify button. A modal will appear on the OctoPrint interface in your browser. Click "Allow"
- Choose what functions you want Enabled/Disabled