# Audio Property Page
## SUMMARY
This sample demonstrates the basics of writing an audio property page and can be used as a basis for writing your own property page. The sample requires the AC97 WDM audio sample driver, which runs on an Intel® motherboard with an integrated AC97 controller such as the Intel 810 Chipset.

After you install the audio driver together with this sample, the property page will appear when you open the device manager and click on the properties for the AC97 WDM audio sample driver. Instead of the usual property sheets, you will see an additional property sheet called ‘Features’ that will display some AC97 codec features.
## BUILDING THE SAMPLE
To build this sample, enter any Windows Server 2003 or Windows XP build environment and run `build –cZ` from the AC97 directory (parent directory). This also compiles the AC97 WDM audio driver sample that is needed for this sample to work.

The INF named ‘AC97smpl.inf’ included in the AC97 subdirectory (parent directory) can be used to install the sample after it has been built. Simply copy the INF and this sample binary and the AC97 driver binary to a floppy disk and then update the driver for the device with the one from the floppy. 

Once the driver has been installed with the INF, the property page sample may be updated by copying the binary into %SystemRoot%\System32 on the target machine, provided that there are no INF changes.
## SAMPLE ISSUES
This sample works with Microsoft® Windows® 2000 (or higher) operating systems. If you want to run this sample on Microsoft® Windows® ME for example, you would need to modify the INF file and write a thunk-layer for the property page, since the device manager makes 16-bit calls into the property page sample.
## ADDITIONAL INFORMATION
The property page sample communicates with the AC97 WDM audio driver sample through a private property. The DLL then fills all dialog fields with the information received from the audio driver. The private property is defined in the header file ‘prvprop.h’.

The private property is exposed in the audio driver as a filter property. As a result of this, we don't have to pass down a KSP_NODE structure but a KSPROPERTY structure (which is missing the node). Add properties to the topology filter if they are generic and not connected with a node.

You can pass down additional information besides the KSPROPERTY structure. Whatever you add after the structure is passed to the topology handler. The "Instance" pointer points to the added data and the "InstanceSize" variable in the PPCPROPERTY_REQUEST structure contains the additional buffer length. The output buffer that was passed in the DeviceIoControl call is the "Value" pointer and "ValueSize" variable.

Use node properties if the property changes values of that node, as in the case of a special 3d node. To do this, define your own GUID and attach that to the node, as for example the KSPROPSETID_AUDIO is attached to volume nodes. Make sure you specify KSPROPERTY_TYPE_TOPOLOGY when you talk with a node and pass at least a KSP_NODE structure down. Everything passed after KSP_NODE is again accessible with the "Instance" and "InstanceSize" variables.
## CODE TOUR
### File Manifest
* AC97prop.cpp   
  * Includes all the code necessary for the sample
* AC97prop.def  
  * To build the DLL
* AC97prop.rc    
  * Property sheet definition
* Makefile       
  * Standard Windows NT makefile
* Readme.md     
  * This file
* Resource.h     
  * Needed for the property sheet definition
* Sources        
  * Dependency information for compiling
* Version.h      
  * Version information

© 2004 Microsoft Corporation
