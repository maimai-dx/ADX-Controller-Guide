
# Setup

This document explains how to set up your controller. It assumes you already have Maimai HDD and segatools installed.

## Assembling

[Here](https://youtu.be/zdHaW_dXxM0?si=nH9nuMTKb5KvfQuN)'s the assemble guide from yuan.

## Setup controller

### 1. Connect it.

To setup controller, connect the controller to pc using included type-c cable.
### 2. Change device port.

And change the ports of device by following step.
 1. Open Device Manager
    - Search > Device Manager > Ports (COM & LPT)
2. Change following Device's Port.
	 - How to change Port
		 - Right click > Properties > Port Settings > Advanced > COM Port Number > Select
     - USB Serial Device (Touch Panel) : COM3
     - USB-SERIAL CH340 (Button LED) : COM21
3. Replug it.
4. Open `mai2.ini` file, and change following values below `[AM]`.
```
Target=1
DummyTouchPanel=0
DummyLED=0
```

Than your device manager should be look like this.  
![](</attachment/image/Setup Controller-Device Manager.png>)

### 3. Update driver.

Default controller driver uses keyboard input. Which is really slow.
So updating driver is recommended, specifically IO4 input.

[Here](https://youtu.be/qDsitksnLpw)'s updating tutoral video.
Tutorial video also includes about installing MelonLoader Mod for HID Input. To just install IO4 input, just ignore it.

[ISPTool program](</attachment/file/driver/ISPTool.zip> "download")  
[MelonLoader + HID Input Mod](</attachment/file/driver/MelonLoader.zip> "download")  

- [IO4 Driver](</attachment/file/driver/WM_DX_V3.04-IO4-1P.bin> "download")
	- After you update it, open `segatools.ini` and go to `[io4]`, add `enable=0` below it like following.
	- ![](</attachment/image/Update driver_IO4_segatools_ini.png>)
- [HID Driver](</attachment/file/driver/WM_DX_V3.00-HID-1P.bin> "download")
	- After you update it, make sure there's no `enable=0` under `io4` in `segatools.ini` file.
	- You should install MelonLoader mod to use it.
- [Keyboard Driver](</attachment/file/driver/WM_DX_V3.00-1P.bin> "download")
	- After you update it, make sure there's no `enable=0` under `io4` in `segatools.ini` file.

After all, you should check once more that device's port is same as step 2.
- USB Serial Device (Touch Panel) : COM3
- USB-SERIAL CH340 (Button LED) : COM21

### 4. Adjust touch sensitivity

Default touch setting is not good. So adjusting touch sensitivity using [ConfigApp](</attachment/file/ConfigApp_V1.0.0.3-20231203.zip> "download") is recommended.
Make sure close the game and re-plug the controller before running this program.
Using it in fullscreen mode is recommended.
After exiting the program, plug and unplug the USB again

Here's the recommended touch sensitivity from yuan. 

![](</attachment/image/Adjust touch sensitivity_Recommended value.png>)

