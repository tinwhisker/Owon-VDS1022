# Owen VDS1022
Run the Owon VDS1022 on OS X (Maybe Linux too)


# Intro
The Owon VDS1022 software is all Java - so why is it Windows targeted?

I saw a few people complaining that it doesn't work on non-Windows, and afaik WINE's USB support is
neither here nor there, I put in a lunch hour to see what it takes.


# Prereqs (Minimal)
- Java 'JRE' installed (Mine is '1.8.0_112' as of writing - nothing specific to this version)

# Prereqs (Additional - For scratch installs)
- Owon VDS1022 software ('1.0.23' as of writing)
- libusbJava.jnilib
- libusbpp-legacy-0.1.4.dylib


# Guide
- Extract the Owon installer. This should give a few folders (fpga, plugins, etc.)
- From a terminal, navigate to that folder, then type:
  - java -jar ./plugins/org.eclipse.equinox.launcher_*.jar
  - i.e. java -jar ./plugins/org.eclipse.equinox.launcher_1.3.0.v20120522-1813.jar
    
- Assuming the software loads:
  - Close the app.
  - Copy libusbJava.jnilib to ./plugins/ch.ntb.usb_0.5.9/
  - Copy libusbpp-legacy-0.1.4.dylib to /opt/local/lib/libusb-legacy/ (Note: On OS X, these folders may need creating)
    
- You can also 'mkdir flash_txt' to allow self calibration to store.

- Plug in the 'scope.
- Re-run the Jar file
- Enjoy!

# Issues
- The app says 'Hardware has changed' every time!
    - Remove flashmemory.txt from ./flash_txt
    
- I followed the above, but no 'scope is found.
or
- I double-clicked the jar file and no 'scope is found.
  - You must run the jar from the app folder root, not the plugin folder!
