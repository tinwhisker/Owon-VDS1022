# OWON VDS1022 & VDS2052* for OS X
## Run the OWON VDS1022 on OS X
### (*VDS2052 is untested)

Manual steps provided to:
- See what I did.
- See how to patch future versions or similar tools.
- Maybe get it to work on Linux too [Debian reported working].

Forks and Pull requests welcome.

OWON VDS © & ™ of OWON Technology Inc. (part of LILLIPUT Group).
This repo, nor I, have no affiliation with OWON Tech or LILLIPUT other than an end-customer.
This is a community effort to simplify use on unsupported platforms.
I provide no warranty, guarentee, support or hope for this script, neither does OWON
If you find bugs in the OWON tool, assume it's your fault until you reliably reproduce and document against a supported platform.

# Versions
2.4.1 - 2018/03/29 - Third release based on 1.0.29
  WIP Edition:
  - Contains some OS X fixups
  - Help files converted from MS Help files to PDF's.
  - More 'native' bootstrapper.
  Issues:
  - USBDriver installer not fixed on this version (Use a non-WIP version to install drivers first)
  - Some file save/load functions fail due to bug in Java runtime - and I haven't patched all functions yet.
  
2 - 2018/03/15 - Second release based on 1.0.29
    Fixes:
        - Updated bootstrap script to use AppleScript (To offer a 'Mac' rights elevation for installing libUSB files)
        - Include missing libUSB files.
        - Fix repo typo. (Yeah, I didn't spot it said 'Owen' for over a year!)
        - Works Out-Of-the-Box on a fresh macOS 10.13.3.

1 - 2016/12/22 - First release based on 1.0.23


# Intro
The OWON VDS software is all Java - so why is it Windows targeted?

I saw a few people complaining that it doesn't work on non-Windows, and afaik WINE's USB support is
neither here nor there, I put in a lunch hour to see what it takes.

I also wanted it to be 'turn-key' - I do many re-installs of OS X, so don't want to chase dependencies, or find that they've gone offline.
So you should be able to just download the .app, drop into Applications and just work.

# Auto Steps:

- Extract the Zip.
- Move the .app to Applications.
- Run.
- Perform calibration and follow steps.

# Known issues:
- I goofed the icon.
- If you open/close the app multiple times, without power cycling the VDS unit, it will sometimes act unpredictably/unstable.

# Manual Steps:

### Prereqs (Minimal)
- Java 'JRE' installed (Mine is '1.8.0_112' as of writing - nothing specific to this version)

### Prereqs (Additional - For scratch installs)
- Owon VDS1022 software ('1.0.23' as of writing)
- libusbJava.jnilib
- libusbpp-legacy-0.1.4.dylib
- libusb-0.1.4.dylib

## Guide
- Extract the Owon installer. This should give a few folders (fpga, plugins, etc.)
- From a terminal, navigate to that folder, then type:
  - java -jar ./plugins/org.eclipse.equinox.launcher_*.jar
  - i.e. java -jar ./plugins/org.eclipse.equinox.launcher_1.3.0.v20120522-1813.jar
    
- Assuming the software loads:
  - Close the app.
  - Copy libusbJava.jnilib to ./plugins/ch.ntb.usb_0.5.9/
  
  OSX:
  - Copy libusbpp-legacy-0.1.4.dylib to /opt/local/lib/libusb-legacy/ (Note: On OS X, these folders may need creating)
  - Copy libusb-0.1.4.dylib to /usr/local/
  
  Debian: (Other Linux flavours untested)
  - apt-get install libusb-java default-jre    [Credit to https://github.com/AbirFaisal]
  
- You can also 'mkdir flash_txt' to allow self calibration to store.

- Plug in the 'scope.
- Re-run the Jar file
- Enjoy!

## Issues
- The app says 'Hardware has changed' every time!
    - Remove flashmemory.txt from ./flash_txt
    
- I followed the above, but no 'scope is found.
or
- I double-clicked the jar file and no 'scope is found.
  - You must run the jar from the app folder root, not the plugin folder!
  
- The bootstrapper appears hung!
    -This is due to it waiting for the Java app to close. Update to a newer version for better aesthetic.
