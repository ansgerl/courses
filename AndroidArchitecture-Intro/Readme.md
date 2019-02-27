# Architecture of Smartphone Operating Systems by Example - Android
<small>By Prof. Dr. Ansgar Gerlicher, Feb. 2019</small>


<!-- slide -->
## Agenda

+ Architektur, Protokolle und Schnittstellen
  + Android Platform Architecture (Platform challenges, OS Layers, Dalvic / ART, Dex Files) 
  + Developer Toolchain (Android Studio, ADB)
  + Android Development Basics 
+ Apps, Services & IPC
  + Intents, Binder, AIDL
+ Kommunikation Apps mit Backend/Cloud -> Informationsflow (Protokolle)
+ Permission / Security
+ „Diagnose in Android Apps“
  + Logging / Fehleranalyse / Debugging

<!-- slide -->

## What is Android?

 + Operating System for ...
	+ ...
	+ ...
	+ ...
	+ ...
	+ ...
	+ ...

<!-- slide -->

![center 60%](./assets/android_devices.png)


 
<!-- slide -->

## What is Android?

+ Operating System for ...
	+ Smartphones
	+ Tablets
	+ Smart Watches
	+ Smart TVs
	+ Infotainment Systems
	+ Or more general: Embedded Systems

<!-- slide -->

## Short Android History

+ July 2005: Google acquires Android Inc.
+ 5\. November 2007: Open Handset Alliance established
+ 21\. October 2008: Google publishes the Android  source code (Apache 2.0 License)
+ 2\. February 2009: T-Mobile G1 / HTC Dream is first available Android hardware in Germany
+ February 2011: Motorola Xoom: First Tablet with Android 3.0 (Honeycomb)
+ 19\. October 2011: Release of Ice Cream Sandwich (ICS, 4.0) on Samsung Galaxy Nexus
+ 9\. July 2012: Release of Jelly Bean (4.1) and Google Nexus 7 Tablet
+ ...

<!-- slide -->

## What comes with Android?

+ Basic system tools, e.g. dialer, address book...
+ Media support: H.264, MP4, MP3, WMA, Ogg...
+ Messaging: SMS, MMS
+ Connectivity: Wi-Fi, GSM/EDGE, UMTS, Bluetooth, NFC
+ 2D/3D graphics (OpenGL)
+ Multitasking
+ Additional Hardware: Camera, GPS, accelerometer, gyroscope, magnetometer...

![center](./assets/android_skateboard.gif)

Image source: giphy.com

<!-- slide -->

# Android Architecture

<!-- slide -->

## Android Platform Challenges

+ Small / cheap devices with
	+ Low processing power
	+ Little memory
	+ Battery driven
	+ Maybe slow networking speed
+ Various hardware (Smartphone, Tablet, Watch, Infotainment, TV, thousands of brands)
	+ Requires platform abstraction

<!-- slide -->

<!-- row -->
<!-- column -->

## Android Platform Architecture
    
+ Based on Linux Kernel (v3.0 since Android 4.x)
+ Hardware Abstraction Layer providing standardized library modules for device's harware
+ Android Runtime (ART) since v5.0 before,  Dalvik VM
+ Native Libraries written in C/C++
+ Java API Framework for normal Android Apps
+ System Apps use the Java APIs
+ [See: developer.android.com](https://developer.android.com/guide/platform/index.html)
    
<!-- column:end -->   
<!-- column -->    
    
![60%](https://developer.android.com/guide/platform/images/android-stack_2x.png)
    
 <!-- column:end -->   

<!-- row:end -->

<!-- slide -->

## Dalvik VM / ART Optimizations

Optimization | Effect
---|---
Combination of multiple Class files in one DEX file | Smaller memory footprint, faster load of the application
Sharing of DEX files between processes (read-only mapping)|Smaller memory footprint, faster load of the application
Byte ordering and word alignment according to local machine (install time)|Faster load of the application DEX file itself still platform independent
Bytecode pre-verification (as much as possible, install time)|Faster load and execution
Install-time optimization of bytecode|Faster execution, still platform independence
Register instead of stack based virtual machine|Faster execution (~30%)

See: http://sites.google.com/site/io/dalvik-vm-internals

<!-- slide -->

## Dex File Format
![center](./assets/dex_file_format.png)

<!-- slide -->

# Android Developer Toolchain


<!-- slide -->

## Android Studio Contains
+ Android SDK
	+ Android APIs 
	+ AVD Manager & Emulator
	+ Android Development Tools
		+ ddms (Dalvik Debug Monitor Service)
		+ adb (Android Debug Bridge) 
		+ dx (.class -> .dex)
		+ aapt (Android Asset Packaging Tool)
+ Android NDK
+ Download [here](https://developer.android.com/studio/index.html)

<!-- slide -->

## Android Debug Bridge (adb)

+ Terminal tool to connect to a device
	+ Find it at (on macOS): `/Users/\<user>/Library/Android/sdk/platform-tools`
+ open shell on emulator 

```

> adb -e shell 

```

+ copy file/dir to device

```

> adb push \<local> \<remote>

```

+ copy file/dir from device

```

> adb pull \<remote> \[\<local>]

```

+ Install package

```

> adb install \<file>

```

<!-- slide -->

# Android Development Basics

+ The Manifest
+ User Interface Layout Files
+ Resources (Strings, Images, etc.)
+ Support Libraries
+ Android Build Process

<!-- slide -->

## Android Manifest

+ It names the Java package for the application (unique identifier for the app)
+ It describes the components of the application (e.g. activities, services, etc.) and names the classes that implement them
+ Defines the Intent messages that they can handle 
+ Declares the permissions 
+ It declares the minimum level of the Android API that the application requires.
+ It lists the libraries that the application must be linked against.
+ ... 

<!-- slide -->

## Android Manifest Structure

````

<?xml version="1.0" encoding="utf-8"?>
<manifest>
    <uses-permission />
	<application>
        <activity>
            <intent-filter>
                <action />
                <category />
                <data />
            </intent-filter>
            <meta-data />
        </activity>
         <service>
            <intent-filter> . . . </intent-filter>
            <meta-data/>
        </service>
	</application>
</manifest>

````

<!-- slide -->