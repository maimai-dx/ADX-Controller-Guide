
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

Then your device manager should be look like this.  
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


## Setup aime reader

There are various ways to setup aime reader.
Depending on the item you purchased, proceed with one of the following steps.

### Setup without aime reader

Segatools provides aime reader simulator in it.
first of all, open `segatools.ini`, check `enable=1` exists under `[aime]`. 
If not, modify or add `enable` to enable it.

![](</attachment/image/NoAimeReader_1.png>)

And open `DEVICE` folder, and create `aime.txt` with 20 random number like below.
Using same value with below is **NOT RECOMMENDED**.

![](</attachment/image/NoAimeReader_2.png>)  
![](</attachment/image/NoAimeReader_3.png>)


### Setup with aime reader

Segatools provides card reader simulator in it. To use own card reader, you have to disable original one.  
first, connect your aime reader to PC.

And change the device connection by following step.

> **Do not modify existing USB Serial Device (COM3) device.** It is touch panel.

 1. Open Device Manager
    - Search > Device Manager > Ports (COM & LPT)
2. Confirm that there's no device is using COM1.
	1. If there's any device using COM1, change it to other any port like `COM2`.
3. Change `USB Serial Device`'s baudrate to `115200`.
    - Right click > Properties > Port Settings > Bits per second : 115200
	    - ![](</attachment/image/WithAimeReader_1.png>)
4. Change `USB Serial Device`'s Port to COM1.
	- Right click > Properties > Port Settings > Advanced > COM Port Number > `COM1`


Then your device manager should be look like this.  

![](</attachment/image/WithAimeReader_2.png>)

Then, open `segatools.ini`, under `[aime]`, modify `enable` to `0` to disable aime reader simulation. 

![](</attachment/image/WithAimeReader_3.png>)

## Setup data server

Data server is used to save play record, rating, etc. If you are too lazy to setup it, there's public data servers. But it can be closed any time. Do whatever you want.

### Setup online server

Setting up an online server is really easy, but please keep in mind that servers can always go down unexpectedly.

To setup online server, just open `segatools.ini`, and change `[dns]`'s `[default]` value to server url you want to setup.

Here's the list of online servers.

| URL        | Supported Version | WebUI |
| ---------- | ----------------- | ----- |
| ea.msm.moe | ?                 | ?     |

### Setup [ARTEMiS](https://gitea.tendokyu.moe/Hay1tsme/artemis)

[ARTEMiS](https://gitea.tendokyu.moe/Hay1tsme/artemis) is the network service emulator for games running SEGA'S ALL.NET service.
You should run it on a maimai pc or a PC using same router with maimai pc.
To use it, download source code from [develop branch](https://gitea.tendokyu.moe/Hay1tsme/artemis/src/branch/develop), and follow the [INSTALL_WINDOWS](https://gitea.tendokyu.moe/Hay1tsme/artemis/src/branch/develop/docs/INSTALL_WINDOWS.md) guide.
And change the `core.yaml`'s `aimedb.key` to `Copyright(C)SEGA`
- This is just a sample key for aimedb configuration.
- It does not imply any copyright or association with SEGA.

To preventing game freeze at specific time everyday, change `core.yaml`'s value to following value.
```yaml
title:
    reboot_start_time: "06:59"
    reboot_end_time: "07:00" # this must be set to 7:00 am for some game, please do not change it
```

And open cmd, type `ipconfig` and find your Internal network IP like starting with `10.~`, `192.~`, `172.~`.
Open  `segatools.ini`, and change `[dns]`'s `[default]` value to server your server IP.

#### Auto start server on start pc
 
Press `Win + R` and type `shell:startup` to open startup folder.  
And create `artemis.bat` with following content. You should modify {Path to artemis} to yours. 
```bat
@echo off
cd {Path to artemis}
start /min cmd /c "python index.py"
```

#### If you installed server at maimai pc and there's no Internal network IP

If you installed artemis server at maimai pc with no router, you are not not able to find Internel network IP. Since maimai does not allow a server with IP `127.0.0.1`, that we need to create a virtual IP using Hyper-V.

First, enable Hyper-V by following this [manual](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v).  

And Open `Hyper-V Manager` and select your `Desktop` and Open `Virtual Switch Manager`.

![](</attachment/image/HyperV_1.png>)

And select `New virtual network switch` > `Internal` > `Create Virtual Switch`

![](</attachment/image/HyperV_2.png>)

Rename it to `maimaidx` and press `OK`.

![](</attachment/image/HyperV_3.png>)

And press `Win + R` and type `ncpa.cpl`, and press `Enter` to open `Network Connections` page.
Then right click `vEthernet (maimaidx)` > click `Properties` > select`Internet Protocol Version 4 (TCP/IPv4)` > click `Properties`

![](</attachment/image/HyperV_4.png>)
![](</attachment/image/HyperV_5.png>)

And modify values like below then click OK > Yes.
Your server IP is now `192.168.2.100`. modify `segatools.ini`, and change `[dns]`'s `[default]` value to this value.

![](</attachment/image/HyperV_6.png>)


### Setup [AquaDX (Unstable)](https://github.com/hykilpikonna/AquaDX)

[AquaDX](https://github.com/hykilpikonna/AquaDX) is multipurpose game server powered by Spring Boot, for ALL.Net-based games.
It is originally created by [samnyan](https://github.com/samnyan), but it is abandoned. Than [hykilpikonna](https://github.com/hykilpikonna)  is back to maintenance and is currently working on BUDDiES update support.
To install AquaDX, [follow this manual](https://github.com/hykilpikonna/AquaDX?tab=readme-ov-file#usage-v1-developmental-preview).

## Setup maimai HDD

maimai is created using unity.
to run the game there's some programs you need to install.

First, Download and install `VisualCppRedist_AIO_x86_64.exe` from [here](https://github.com/abbodi1406/vcredist/releases).

Second, open `config_commons.json` file and modify `credit` part like below. This enables freeplay.
```json
"credit": {
    "enable" : true,
    "max_credit" : 24,
    "config" : { "freeplay" : true }
},
```

Third, double click `start.bat` to start game and wait.
You'll get stuck on this screen.

![](</attachment/image/MaimaiHdd_1.png>)

Press the second circular button on right side to enter this menu,
And disable following menu's value using number 1, 4, 5 button on main display.
Then select `終了` to quit menu.

![](</attachment/image/MaimaiHdd_2.png>)
![](</attachment/image/MaimaiHdd_3.png>)

Then you'll get this screen.

![](</attachment/image/MaimaiHdd_4.png>)

#### Auto start maimai on start pc
 
Press `Win + R` and type `shell:startup` to open startup folder.  
And create `maimai.bat` with following content. You should modify {Path to maimai start.bat} to yours.
```bat
cd {Path to maimai start.bat}
start.bat
```


Congratulations! You finllay finished setup game. You can create an account and enjoy the game by pressing the `enter` key or tapping the card.  
Enjoy!