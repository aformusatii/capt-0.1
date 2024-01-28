# CAPT Linux driver for LBP-810 and LBP-1120

Original source https://www.boichat.ch/nicolas/capt/

In this repo I just fixed the error you get while compiling:
```sh
/temp/capt-0.1 $ make
gcc  -O2 -g capt.c -o capt
/usr/bin/ld: /tmp/cc0g34NW.o: in function `out_packet_buf':
/home/pi/temp/capt-0.1/capt.c:167: undefined reference to `errorexit'
/usr/bin/ld: /tmp/cc0g34NW.o: in function `out_packet':
/home/pi/temp/capt-0.1/capt.c:254: undefined reference to `errorexit'
/usr/bin/ld: /home/pi/temp/capt-0.1/capt.c:203: undefined reference to `errorexit'
/usr/bin/ld: /home/pi/temp/capt-0.1/capt.c:211: undefined reference to `errorexit'
/usr/bin/ld: /home/pi/temp/capt-0.1/capt.c:245: undefined reference to `errorexit'
/usr/bin/ld: /tmp/cc0g34NW.o:/home/pi/temp/capt-0.1/capt.c:254: more undefined references to `errorexit' follow
collect2: error: ld returned 1 exit status
make: *** [Makefile:13: capt] Error 1
```

Tested on 
* Rasberry Pi 1 Model B (very slow, about 3 minutes to print a page, barely usable)
* Rasberry Pi 3 Model B (speed is acceptable)

## Linux Canon CAPT driver
-----------------------
In this package there is a linux driver for Canon printer using CAPT protocol.
The general structure of the application is based on Rildo Pragana's driver for Samsung ML-85G, see : http://pragana.net - "Adventures in Linux Programming".
It should support both A4 and Letter sized paper, but I only tested it with A4 sized paper.

## Install
-------
```sh
git clone https://github.com/aformusatii/capt-0.1.git
cd capt-0.1
# Compile driver
sudo make
# Install driver files
sudo make install
# You need to have USB Printer support in your kernel. Install the needed module via
sudo modprobe usblp
# And a new device should appear (/dev/usb/lp0). 
# Change permissions to give access to the printer to users.
# Tthis is also needed for CUPS to work.
sudo chmod a+rw /dev/usb/lp0
```

## Install in CUPS
---------------

Follow the instructions presented on this page: http://www.linuxprinting.org/cups-doc.html
When installing, do not select an USB port, but a dummy serial port (for example Serial Port #8).
To align the margin, change TopSkip and LeftSkip parameters.
