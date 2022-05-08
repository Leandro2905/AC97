# Audio Control Panel Application Sample
## SUMMARY
This sample illustrates the basics of writing a control panel application. The sample only works in conjunction with the AC97 property page sample, which in turn requires the AC97 WDM audio driver sample. The AC97 WDM audio driver sample runs on an Intel® motherboard with integrated AC97 controller (for example, the Intel 810 chip set). 

Microsoft discourages the use of control panel applications because cluttering of the control panel is confusing to most users. Most of the functionality that you might want to provide can be added in a property sheet that is added to the property page of your device. To learn how to write a property page DLL, see the proppage sample. 

Microsoft also discourages the use of system tray programs (programs that get displayed in the notification area of the system tray). These programs are running all the time and eat up resources. The notification area of the system tray is for notifying the user of events only. 

If you find that your device driver's property page is unable to give you all the functionality or configuration options that you need, this sample shows you how to write a control panel application that might provide more extensive configuration options and greater functionality.
## BUILDING THE SAMPLE
To build this sample, enter any Microsoft® Windows® Server 2003 or Windows XP build environment and run the command `build –cZ` from the AC97 sample directory (parent directory). This command also builds the AC97 WDM audio driver sample and the property page sample that are needed to work with the control panel sample. 

The INF file AC97smpl.inf in the AC97\driver subdirectory can be used to install the AC97 property page sample and the AC97 WDM audio driver sample that is needed for this sample. Simply copy the INF file, the AC97 driver binary file, and the property page sample binary file to a floppy disk and then update the driver for the device with the one from the floppy. After updating the driver, you can install the control panel application by simply copying the binary file to the %SystemRoot%\system32 directory.
## SAMPLE ISSUES
This sample only works with Windows 2000 (or later) operating system due to the restrictions of the AC97 property page sample.
## ADDITIONAL INFORMATION ABOUT THE SAMPLE
This control panel application simply creates a dialog and loads the AC97 property page sample that in turn provides a property sheet to this dialog. The control panel application then displays the dialog. Of particular interest in this sample is the code that finds the AC97 WDM audio driver in the system because this information needs to be passed to the AC97 property page.
## CODE TOUR
### File Manifest
* ac97cpl.cpp    
  * Includes all the code necessary for the sample
* ac97cpl.def    
  * To build the CPL file
* ac97cpl.ico    
  * The icon
* ac97cpl.rc     
  * Property sheet definition
* makefile       
  * Make file
* readme.md     
  * This file
* sources        
  * Dependency information for build utility
* version.h      
  * Version information

© 2004 Microsoft Corporation
