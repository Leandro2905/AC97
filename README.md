# AC97 Sample Driver and Related Code Samples
## SUMMARY
This directory contains a sample AC97 adapter driver and several related code samples. The samples are contained in the following subdirectories:
### Subdirectory
* cpl
  * This subdirectory contains the sample code for a control panel application. The application displays the property page for your AC97 device. This application requires that the property page sample and the AC97 WDM audio driver sample be installed.
* driver
  * This subdirectory contains the AC97 sample driver. This sample is a WDM audio adapter driver that runs on an Intel® motherboard with an integrated AC97 controller. The adapter driver incorporates a wavePci miniport driver for the AC97 controller's wave audio device. 
* INFViewer
  * This subdirectory contains an HTML version of the AC97 driver's INF file. The HTML file supports easy browsing of the INF file's contents by providing hot-linked references to INF sections and to keyword definitions.
* proppage
  * This sample shows how to write a property-page DLL that gets loaded by the device manager when a user elects to display the properties of your device. In addition to displaying the default property sheets, the device manager also displays the property sheet that is defined in the sample. This sample requires that the AC97 WDM audio driver sample be installed.

These samples need to be compiled with the Microsoft® Windows® Server 2003 or Windows XP build environment but are binary compatible with older operating systems such as Windows 2000. To build the samples, enter any Windows Server 2003 or Windows XP build environment and run the command `build ?cZ` from this directory. The AC97 sample driver also runs in Windows 98 Second Edition or Windows Me, but the property page DLL and control panel application do not.

The header file prvprop.h in this directory defines the private property used by each of the samples. The INF file in the AC97\driver directory installs all of the samples in the subdirectories. For more information, see the readme.htm files in each subdirectory. 

## ADDITIONAL INFORMATION ABOUT THE INF FILE
In Windows 2000 and later, the INF file in the AC97\driver directory installs both the AC97 sample driver and the property page sample. In Microsoft Windows 98 Second Edition and Microsoft Windows Me, the INF file installs only the AC97 WDM audio driver sample. A migration DLL (migrate.dll) is needed for a WDM audio driver that has been installed in Microsoft Windows 98 Second Edition or Microsoft Windows Me to survive the upgrade to Microsoft Windows 2000 or later. For more information on device driver migration, see %BASEDIR%\src\setup\devupgrd\devupgrd.doc.

© 2004 Microsoft Corporation
