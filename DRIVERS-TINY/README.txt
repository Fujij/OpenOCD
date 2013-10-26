--- DRIVERS INSTALLATION GUIDE ---

*** This folder contains drivers for the following products:
 - ARM-USB-OCD
 - ARM-USB-OCD-H
 - ARM-USB-TINY
 - ARM-USB-TINY-H
 - ARM-JTAG-EW
  
*** Supported OS:
 - Windows XP x86, x64
 - Windows Vista x86, x64
 - Windows 7 x86, x64

*** Driver version
 - LibUSB version 1.2.2.0, http://sourceforge.net/projects/libusb-win32/files/
 - USB serial port driver FTDI 2.08.08, 16 November 2010, http://www.ftdichip.com/Drivers/VCP.htm
	
*** How to install the drivers:
	Installation should be pretty straightforward. Plug in the your device in the USB port, you should be prompted to provide driver files for the device. Choose "Install from a specific location (Advanced)", then choose the folder 'olimex-libusb-1.2.2.0' and click Next. A search for compatible drivers is initiated and your device should be installed. 
	IF YOU ARE USING 'ARM-JTAG-EW' :
		That's it, nothing more to do.
	
	IF YOU ARE USING 'ARM-USB-TINY' or 'ARM-USB-TINY-H' :
		Please repeat the operations for the second interface of the device. You should end up with 2 devices displayed in Device manager in the section "libusb-win32 devices".
		
	IF YOU ARE USING 'ARM-USB-OCD' or 'ARM-USB-OCD-H' :
		In order to install drivers for the serial port when prompted again for drivers choose "Install from a specific location (Advanced)", then choose the folder 'CDM20808' and click Next. A search for compatible drivers is initiated and your device should be installed. Up to now you have installed the USB serial converter device, now you will actually install the serial port (COMX). Again you will be prompted to provide drivers, choose "Install from a specific location (Advanced)", then choose the folder 'CDM20808' and click Next. A search for compatible drivers is initiated and your device should be finally installed. Open a beer and relax :)
	
	*Note: In the installation process you may be warned that driver files are not digitally signed by Microsoft, please ignore these rather annoying messages.
	
*** Troubleshooting (USE ON YOUR OWN RISK!)
	In some cases the procedure described above is not successful and no driver is installed for your device. In such a case after choosing "Install from a specific location (Advanced)" select "Don't search. I will choose the driver to install". Then select "All devices" and press the button "Have disk". If installing the first subdevice (or the second in a -TINY JTAGS) choose the file "driver.inf" in folder 'olimex-libusb-1.2.2.0' and continue discarding the warnings. If installing the serial port (whick is the second subdevice) drivers choose file 'ftdiport.inf' in folder 'CDM20808'.
	
	If things get extremely messy you should clean your system completely for any information about a specific device and reinstall driver from the very beginning. This is a universal way to remove any usb driver. To do so download "FTClean - Driver Removal Utility" from:
	http://www.ftdichip.com/Support/Utilities/FTClean.zip
	
	Start FTClean.exe and choose VID: Other and enter Olimex's VID: 0x15BA. For the PID value use any of the following:
		- ARM-USB-OCD		0x0003
		- ARM-USB-OCD-H		0x002B
		- ARM-USB-TINY		0x0004
		- ARM-USB-TINY-H	0x002A
		- ARM-JTAG-EW		0x001E (0x001F)
		
	Then reinstall driver the usual way.

*** Information, updates and support:
	http://www.olimex.com/
	email: support@olimex.com
	
*** Last edit
	23 November 2010

Enjoy :)