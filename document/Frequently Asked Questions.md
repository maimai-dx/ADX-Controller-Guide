
## I cannot start game.

### Game is stuck on black background + blue circle
If you stuck at this screen, you should install vcredist. See [Setup](/document/Setup.md)

![](</attachment/image/CannotStartGame_1.png>)

### Game is stuck on black screen. 
If you stuck at this screen, and your CPU is intel 10th Gen or above, there's a possibility that it was caused by [OpenSSL-Sha-Crash-Bug](https://www.intel.com/content/www/us/en/developer/articles/troubleshooting/openssl-sha-crash-bug-requires-application-update.html).
To fix it, open `start.bat` with notepad and add this command at first. 
```bat
set OPENSSL_ia32cap=:~0x20000000
```

![](</attachment/image/CannotStartGame_2.png>)

### I cannot start game as soon as install MelonLoader.
Install this [MelonLoader](</attachment/file/driver/MelonLoader.zip> "download") instead.

## Game is too laggy at specific time (19:00~20:00)
If you are using ARTEMiS and following message spams to console, it is becuase of Maintenance time of game.
Open `artemis\titles\mai2\dx.py`, modify `rebootStartTime`, `rebootEndTime` value and restart server.

![](</attachment/image/TooLaggy_1.png>)

## Touch Screen / Button LED does not work

Replug controller and restart game.
If the problem does not solved, check and change device's COM port again. (See [Setup](/document/Setup.md))
Becuase of bug, window just changes device port randomly. If you going to change back to valid port, window can say to you that port is already in use. But that's a bug. just ignore it.

## Button does not work

Replug controller and restart game.
If the problem continues, the solution may depend on your firmware.

### If you are using Keyboard Input
- open notepad and press button. you should get wedcxzaq.
- Open `segatools.ini` file. Check there's should be no `enabled=0` under `[io4]`.
### If you are using HID Input
- Check you installed HID Input unity mod.
- Check MelonModLoader console starts on game startup.
- Open `segatools.ini` file. Check there's should be no `enabled=0` under `[io4]`.
### If you are using IO4 Input
- Open `segatools.ini` file. Check there's `enabled=0` under `[io4]`.
