# Complete Nethunter tutorial

**Author**: Mroczek

- [LinkedIn](https://www.linkedin.com/in/igor-mroczkowski-75a420331/)

---

## Need to do
- download any [roms](https://github.com/notthehiddenwiki/NTHW/blob/nthw/Android/roms.md) from recommended list
- download [Kali Nethunter Generic](https://www.kali.org/get-kali/#kali-mobile)
- download [Magisk](https://github.com/topjohnwu/magisk/releases)

## Installation of custom recovery
1. install adb drivers for your phone, search for specific drivers e.g samsung. [https://developer.android.com/studio/run/win-usb](https://developer.android.com/studio/run/win-usb?hl=en) 
2. connect your phone via usb cable. (make sure cable is working)
3. on your phone, go to settings next *about phone/android version* hit build number 5 times.
4. go to developer settings, click usb debugging.
5. connect phone via usb to your device.
6. open cmd in platform-tools patch, and type `.\adb devices` and accept all debugging popUPs on your phone.  
7. enter fastboot or any other bootloader, press volume down and shutdown in this same time, wait until phone reboot to bootloader.
8. type `.\fastboot device` in your pc command line, when your appear you can go next, if your phone doesn't appear try to install other usb drivers like xiaomi or Samsung
9. follow instruction from [https://wiki.lineageos.org/](https://wiki.lineageos.org/) to flash your OS (all in one place, 100% you will find your device) USE YOUR ROM RECOVERY
 
## Installing nethunter generic
1. change file extension from magiskXX.apk to magisk.zip
2. enter to your recovery, click "Factory reset" and "apply update" next  "apply from adb"
3. type in cmd `.\adb sideload patch-to-your-magisk.zip` wait until phone flash magisk and reboot to android, if magisk app not appeared, just drag to your phone magisk.apk and open it
4. open magisk-app in android, click install button on home page, click "direct" option and reboot
5. in magisk-app, click settings button next scroll down and hit "zygisk" and reboot
6. drag nethunter file on your device, click modules page on magisk-app, click install from storage and select nethunter generic. ALL done
