The point of this repository is to help setup OpenOCD with the Olimex JTAG-UTB-TINY however where I can think of the differences for the UTB-TINY-H I will point that out.

Basically Olimex is a shit company. They are useless when it comes to helping with their products and although they claim to support the open source community they dont - I suspect they are getting back handers from larger companies.

However they do make cheap JTAG's...

This is a description for Windows but Linux users - i plan on updating to talk about this, although if you are a linux user you should be good enough to "port" the following over. Mac users, I dont know for you, all I know is Mac is based on Free-BSD and therefore should be basically like setting up for Linux.

So buy either of the above two products.

Firstly install the latest version of open-ocd. For me that was 0.7.0

For the USB-TINY download from here the folder called DRIVERS-TINY

Plug in your jtag and wait until the computer cant install the drivers.
Go to device manager and for the first of the two Olimex devices locate the driver in the appropriate folder
Point it at the olimex-libusb folder in DRIVERS-TINY...
Install it, and do it for the other device.

Once done go to C:\ [location of openocd installation]
In the folder scripts is a folder called interface.

In there find the olimex-arm-usb-tiny.cfg - if its not there make one and put this in it:

	#
	# Olimex ARM-USB-TINY
	#
	# http://www.olimex.com/dev/arm-usb-tiny.html
	#
	interface ft2232
	ft2232_device_desc "Olimex OpenOCD JTAG TINY A"
	ft2232_layout olimex-jtag
	ft2232_vid_pid 0x15ba 0x0004

If you are using the TINY-H make a file (if it doesnt exist) called olimex.arm-usb-tiny-h.cfg and put this in it:

	#
	# Olimex ARM-USB-TINY-H
	#
	# http://www.olimex.com/dev/arm-usb-tiny-h.html
	#
	interface ft2232
	ft2232_device_desc "Olimex OpenOCD JTAG ARM-USB-TINY-H"
	ft2232_layout olimex-jtag
	ft2232_vid_pid 0x15ba 0x002a

Finally download from here openocd.cfg and put it in the openocd-0.x\bin folder.

At the top of that file there are the lines:

source [find interface/olimex-arm-usb-tiny.cfg]
source [find target/lpc1788.cfg]

If you are using a different target, go into the target folder - in the scripts folder you were in earlier, and find the name for your target.
If you are using the TINY-H then change the cfg file to that file.
Lastly, for convenience only rename the openocd-0.x.x.exe to openocd.exe

Finally to test everything, open a command prompt (you can put openocd.exe on the enviroment PATH if you know how, Im not going to explain that here) navigate to the openocd-0.x.x\bin folder and type in:
openocd -f interface/olimex-arm-usb-tiny.cfg -f target/lpc1788.cfg -c "shutdown"

If all goes to plan you should get something like:

Open On-Chip Debugger 0.7.0 (2013-05-05-10:41)
Licensed under GNU GPL v2
For bug reports, read
        http://openocd.sourceforge.net/doc/doxygen/bugs.html
Info : only one transport option; autoselect 'jtag'
adapter_nsrst_delay: 200
jtag_ntrst_delay: 200
adapter speed: 10 kHz
cortex_m3 reset_config vectreset
cortex_m3 reset_config sysresetreq
shutdown command invoked
Info : clock speed 10 kHz
Info : JTAG tap: lpc1788.cpu tap/device found: 0x4ba00477 (mfg: 0x23b, part: 0xba00, ver: 0x4)
Info : lpc1788.cpu: hardware has 6 breakpoints, 4 watchpoints

Possible issues here are you get ftdi device not found. Three options:
1. Your JTAG is broken. It took me 2 weeks to figure that out.
2. You buggered up the driver installation. In that case you need to use the FTDIClean.exe application, also included here. Go to device manager uninstall the drivers for the olimex device, unplug the olimex device run FTDIClean.exe and then:

Change the VID(hex) to other
In the text box put 15ba
In the PID (Hex) text box, for the USB-TINY put 0004, for the TINY-H put 002a

Rerun the driver installation.

Option 3, and this only seems relevent for the USB-TINY, in the cfg file, try changing the line:
ft2232_device_desc "Olimex OpenOCD JTAG TINY A"
to
ft2232_device_desc "Olimex OpenOCD JTAG TINY B"

I've heard that can fix it...

Finally to flash the device try:

openocd.exe -f openocd.cfg -c "[<hexfile name>.hex; exit]"