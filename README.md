# Driving-Force-Pro
How to install Logitech Driving Force Pro Wheel on Linux Ubuntu 14.04

So far, the [LTWheelConf](https://github.com/TripleSpeeder/LTWheelConf) maybe is the best solution to get following wheels working on Linux:
This tool allows you to change various settings of the Logitech racing wheels
-> Driving Force
-> Momo Racing
-> Momo Force
-> Driving Force Pro
-> Driving Force GT
-> G25
-> G27

Available options:
-> set wheel to "native" mode (support separate axes and clutch pedal, H shifter, full 900 degree rotation)
-> Set wheel rotation range
-> Set autocenter force and rampspeed
-> Set ForceFeedback gain
  
Compile guide

You can easily compile LTWheelConf using the following commands:

Get some dependencies (for Ubuntu 14.04 x86)

$ sudo apt-get install libusb-1.0-0-dev git


Download the source

$ git clone https://github.com/thk/LTWheelConf.git


Build the source

$ cd LTWheelConf

LTWheelConf$ make
LTWheelConf$ ls
You should now have an executable named ltwheelconf.


Install 

LTWheelConf$ cp ltwheelconf /usr/local/bin/ 

List all found/supported devices

LTWheelConf$ sudo ltwheelconf --list


Supported wheel shortname values:

    'DF' (Driving Force)
    'MR' (Momo Racing)
    'MF' (Momo Force)
    'DFP' (Driving Force Pro)
    'DFGT' (Driving Force GT)
    'G25' (G25)
    'G27' (G27) 


Set wheel to native mode

LTWheelConf$ sudo ltwheelconf --wheel <your-wheel-shortname> --nativemode


Set wheel rotation range of 900 degrees

LTWheelConf$ sudo ltwheelconf --wheel <your-wheel-shortname> --range 900


Examples

Put wheel into native mode:

LTWheelConf$ sudo ltwheelconf --wheel G25 --nativemode

Set wheel rotation range to 540 degree:

LTWheelConf$ sudo ltwheelconf --wheel G27 --range 540

Set moderate autocenter:

LTWheelConf$ sudo ltwheelconf --wheel DFP --autocenter 100 --rampspeed 1

Disable autocenter completely:

LTWheelConf$ sudo ltwheelconf --wheel G25 --autocenter 0 --rampspeed 0

Set native mode, disable autocenter and set wheel rotation range of 900 degrees in one call:

LTWheelConf$ sudo ltwheelconf --wheel DFGT --nativemode --range 900 --autocenter 0 --rampspeed 0


Now you can configure the steering wheel directly from Euro Truck Simulator 2. To test and calibrate the steering wheel outside ETS2 you can use jstest-gtk

Add UDEV rule

It is possible to add a rule to UDEV to automatically invoke LTWheelConf when the steering wheel is connected.

This can be done using the following command (use the correct shortname instead of <your-wheel-shortname>!):

LTWheelConf$ echo 'ATTRS{idVendor}=="046d", ATTRS{idProduct}=="c294", RUN+="/usr/local/bin/ltwheelconf --wheel <your-wheel-shortname> --nativemode --range 900"' | sudo tee -a /etc/udev/rules.d/90-logitech-wheel.rules

Now you need to restart UDEV:

LTWheelConf$ sudo service udev restart 
