# AC97 WDM Audio Driver Sample
## SUMMARY
This sample driver demonstrates the basics of writing a WDM audio driver. The sample driver should work with any AC97 codec that is connected to an Intel® motherboard with an integrated AC97 controller (for example, the Intel 810 chip set). The sample driver supports multi-channel audio and builds a mixer topology to represent the data paths in the AC97 codec that is in the system. 

The functionality of the sample driver can be expanded to support non-AC97 design features or to convert the driver to use a different DMA engine. For more information, see the DRIVER ISSUES section below.
## BUILDING THE SAMPLE
To build this sample, enter any Microsoft® Windows® Server 2003 or Windows XP build environment and run `build –cZ` from the main AC97 sample directory (parent directory). 

The INF file AC97smpl.inf in this directory can be used to install the sample driver once it has been built. Simply copy the INF and the driver binary to a floppy disk and then update the driver for the device with the one from the floppy. Note that the INF file tries to install the proppage sample and might try to find additional binaries. For more information, see the readme.htm file in the main AC97 sample directory (parent directory). 

After the INF file has installed the driver, you can update and test new versions of the driver by simply copying the driver binary file into the directory %SystemRoot%\system32\drivers on the target machine and rebooting. This technique should be sufficient unless you also make changes to the INF file.
## DRIVER ISSUES
* At the time of writing, there is no AC97 implementation available for Alpha or IA64 machines. Thus, the DDK sample source does not install on Alpha or IA64 machines. 
* This driver supports the old Intel 810/820/840 implementation as well as the new Intel 815/820 implementation (82801BA/BAM). This new chip set supports multi-channel AC97 codecs, but the sample driver runs satisfactorily only on codecs that are 100-percent AC97-compatible. The double-data-rate playback (for example, at 96 kHz) feature is unsupported in those chip sets and therefore unsupported in the driver. 
* The AC97 low-priority microphone recording capability is disabled. You can record using the microphone just as you would record from any other source (for example, a CD) by using the normal recording selector, but the second recording line that is optionally defined in the AC97 specification is disabled. 
* The AC97 inputs that are reported to the operating system can be disabled through the INF file. In one section of the INF file, you can disable specific input lines of the codec that are not attached to any adapters. 
* This driver works only with Windows 2000 and later and with Windows 98 Second Edition and Windows Me. It will neither run nor install on the original release of Microsoft Windows 98. 
* Due to hardware constrains in the Intel 440MX chip set, the sample driver cannot run reliably on this chip set. Therefore, please do not add Plug and Play device-identification strings that contain PCI\VEN_8086&DEV_7195.
## CODE TOUR
### File Manifest
* ac97reg.h      
  * Definition of the AC97 registers
* ac97smpl.inf   
  * Set-up information
* ac97smpl.rc    
  * Resource file containing version information
* adapter.cpp    
  * Connects driver with the system
* adapter.h      
  * Header file for adapter.cpp
* common.cpp     
  * Common object used by all miniports
* common.h       
  * Header file for the common object
* debug.h        
  * Debug output support
* guids.h        
  * Private GUIDs used by the driver (name definitions)
* ichreg.h       
  * Defines the registers of the Intel AC97 interface (AC97)
* ichwave.cpp    
  * Implementation of the stream object (DMA programming)
* ichwave.h      
  * Header file for the stream object
* makefile       
  * Make file
* mintopo.cpp    
  * Implementation of the topology miniport
* mintopo.h      
  * Header file for the topology miniport
* minwave.cpp    
  * Implementation of the wavePci miniport
* minwave.h      
  * Header file for the wavePci miniport
* prophnd.cpp    
  * Implementation of the property handler (part of the topology miniport)
* shared.h       
  * Header file shared by every C++ source file
* sources        
  * Dependency information for compiling

© 2004 Microsoft Corporation
