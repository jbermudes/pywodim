PyWodim - A python module for the linux CD burning program wodim
Author: Jess Bermudes

=======================
 License
=======================

Copyright (C) 2008 Jess Bermudes

License GPLv2+: GNU GPL version 2 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extend permitted by law.

=======================
 Usage 
=======================

pywodim.py [OPTIONS] [ISOFILE]
Burn a CD and ensure its data integrity using wodim

OPTIONS:
  --dev			the target burning device
  --pre			pre-burn verification of FILE's MD5 sum
  --post			post-burn verification of disc's MD5 sum
  --dummy			turns off drive's laser for test burn
  --help			display this help and exit
  --version		output version information and exit
  
When pywodim is ran as a python script, it can be used to burn a CD.

While it may be useful as a stand-alone script, the main purpose of the 
free-standing code is to offer a glimpse into a sample usage of the module 
functions.

The module provides the ability to query disc/drive status and to data 
verification checks prior to burning and again after a burn to ensure a proper 
burning.

The pre-check assumes that there is an MD5 file in the same directory as the 
ISO. This file should be the output of md5sum on the file in question.

For instance, if you are attempting to burn test.iso, you must provide 
test.iso.md5. You can get a file like this by running:
md5sum test.iso --binary >> test.iso.md5

The post-check was designed to be useful for testing Ubuntu CDs and thus assumes
that the md5sum information lies in the root of the CD directory.

It can also be used as a module for integrating into your own projects.
See the listing of module functions and read the source for more information.
  
  
=========================
  Known Bugs
=========================
  
  The final eject does not work 100% of the time. 
  For some reason the drive is sometimes still in use even
  after a cool-down wait, so if it doesn't eject, let the program
  exit, then eject the disc.
  
 ========================= 
  Behind the Scenes
 =========================
 
	Pywodim is a Python module for burning an ISO file to disc using wodim
	Most of the heavy lifting is done by the following linux programs:
	
	wodim   - does the actual burning
	md5sum  - verifies data integrity
	mount   - checks for disc mount
	eject   - opens/closes drive tray
	volname - gets the disc's volume name
	mount	- for testing the status of a device mount
	grep	- for determining certain output results

	PyWodim also makes extensive use of the Linux CD-ROM
	standard as described in /usr/include/linux/cdrom.h
	in order to talk to the drive and query its status
	via ioctl commands.
	
=========================
 Module Functions
=========================

To learn more about a particular function, check out the docstring or read the source.

burn(isoFile, device=None, isRealBurn=False, ejectAfter=False, speed=None)
closeTray(device="")
getCDVolumeName(device)
getCDDeviceDescriptor(device)
getDefaultDevice()
getDiscMountPoint(device)
getMediaChangedState(device)
isBlankInserted(device)
isMediaInserted(device)
isTrayOpen(device)
openTray(device="")
queryDisc(device)
queryDrive(device)
verifyDisc(mountPoint)
verifyImage(isoFile, md5File)
waitForDiscMount(device, maxWait=0)
waitForMedia(device, maxWait=0)

