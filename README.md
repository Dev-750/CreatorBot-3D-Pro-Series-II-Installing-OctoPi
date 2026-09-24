# CreatorBot 3D Pro Series II - Installing OctoPi
OctoPi, OctoDash, Touch Drivers, etc.

# Introduction

If you have a CreatorBot 3D Pro Series II, wow that's a mouthful, and the current PrinterWorks OS isn't working you've come to the right place. This will show you how to get your printer back up and running with OctoPrint.

## Setup Used
- Linux machine running Ubuntu 24
- Connected to Pi via Wifi
- Pi controlled via SSH

# Creating the Image
1. You will need to Format the Raspberry Pi's SD card or get another micro SD (8-32GB). It must be FAT32.
2. Install the Raspberry Pi Imager. On a debian terminal you can us `sudo apt install rpi-imager`
3. In the Imager, set the OS under "Other (Specific)" -> "3D Printing" -> select "OctoPi (Stable)"
4. Configure image options
	1. Set Hostname, Username, password
	2. Wifi connection
	3. Location
	4. Keyboard layout
5. Write the image to the SD card

- [More instructions on OctoPrint.org](https://octoprint.org/download/)
- [OctoPi Github](https://github.com/guysoft/OctoPi)
# Running OctoPrint
Now that OctoPi is on the Pi it will Start the OctoPrint server which can be accessed from a Browser on the same network to control the printer.

1. To access OctoPrint, open your browser and type in one of three options:
- `http://octopi.local`
- `http://<custom-hostname>.local`
- `http://<pi's-IP-address>.local`

Using the IP address seems to work the best. To find it type:
```bash
hostname -I
```
 in the Pi's Terminal. **You will either need a keyboard, SSH, or Putty, etc**

To SSH into the Pi type: 
```bash
ssh <username>@<hostname.local or IP>
``` 
and enter the Password

2. Once the interface loads, create an account.
3. Now you will see all of your printers metrics and options and be able to control and print from here.

# OctoDash Install

Since this printer comes with a touch screen, you might aswell have a GUI on it. OctoDash gives you access to key controls right from the touch screen

1. Update the system: `sudo apt update`
2. Upgrade packages; `sudo apt upgrade`
3. Enable Auto-login console in `raspi-config`
4. Reboot: `sudo reboot`
5. Use the script below to Install OctoDash

This script is also on the OctoDash Github

```bash
bash <(wget -qO- https://github.com/UnchartedBull/OctoDash/raw/main/scripts/install.sh)
```

6. Follow the selection prompts. The last prompt will reboot the Pi

[OctoDash Github](https://github.com/UnchartedBull/OctoDash)

[@ChrisRiley Installation Video](https://m.youtube.com/watch?v=kwo3HMBnqC4)

# Touch Driver Install

The screen is a genwric HDMI resistove/capacitive touch display that is connected via SPI.

1. `sudo raspi-config` -> Interface Options -> SPI -> Enable -> Reboot
2. Enter the config file `sudo nano /boot/firmware/config.txt`
3. Add the following to the bottom of the file: 
   
```txt
dtoverlay=ads7846,cs=1,penirq=25,penirq_pull=2,speed=50000,keep_vref_on=0,swapxy=0,pmax=255,xohms=150,xmin=200,xmax=3900,ymin=200,ymax=3900
```

4. Save (`Ctrl+O`, `Enter`) and exit (`Ctrl+X`), then reboot

# OctoDash Setup

- **Feed Length**: 80-120mm
- **Feed Speed**: 3-5mm/s

*If it stops short of extruding at the nozzle, increase length; if it grinds/skips, decrease speed*

- **API Key**: Click the verify button. A modal will appear on the OctoPrint interface in your browser. Click "Allow"
- Choose what functions you want Enabled/Disabled
