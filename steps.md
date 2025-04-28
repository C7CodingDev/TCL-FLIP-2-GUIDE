<!-- This is for the HTML version only! -->
# Pre-Reqs:
In order to install anything onto the Flip2, you're going to need a few things.

I highly recommend using the ones provided in the repo, however, I do provide links to downloads for those who don't trust aha.

## Install Details
You will need android ADB tools. You can either directly download them here, or download android studio which is more convenient but takes up more space.

What is NeutronScott's Magisk.img?
NS Magisk 2.5 boot.img is the code modification that is flashed to allow installations of apks. This is good for barebones installations

## What is NeutronScott Recovery?
NS Recovery.img is the recovery image. You likely won't need it. It adds the following utilities: su, busybox, e2fsck, tune2fs, dmctl, lpp. I'll be honest, I don't know what they do but likely it's beneficial. I'm sure there's a minute storage difference, but oh well.

## What is MTKFastboot?
MTK Flashboot is the software that puts the device into fastboot mode. Not much more to say here.

## Why Aurora Store?
Personally, I prefer Aurora over other google play front ends. Being able to spoof my device model fixes many problems I have faced getting apps onto the device. Aurora Store (GPlay Alternative)
First off, you're going to need to enable ADB. That is done by entering `*#*#33284#*#*`. Once you have entered that and ADB is enabled, we can start the fastboot.

# Step 1 - Fastboot
Download the Pre-Reqs Above. . Download either neutronscott recovery, or magisk and insert it in the ADB Directory

Download the VB Meta files + AutoBooter and put them in your ADB directory

Install the fasboot (mtk) drivers and reboot

#Step 2 - Flashing
Turn off your flip 2

Open the Auto Booter by opening a terminal and running it by dragging the file over. In this case, I am using ./mtkfastboot.exe

Plug your phone in.

Some transparency here, my Razer Blade 14" 2021 refused to work with the autobooter, and I cannot explain why. I resorted to an old intel-based laptop and it seemed to have worked. If someone else (AMD) has experienced this, please let me know! Otherwise, it was likely a fluke on my end.
~~Later me here: this is an issue with ALL Ryzen-based devices. You can try this fix however that didn't work for me. I also tried this, yet again, that didn't work.~~
Even later me here: more in-depth research has introduced another theory; this is a USB 3.0 issue. If you have a 2.0 hub, a USB extender that's 2.0, or something else that's 2.0, this likely will work.

Once your phone is in fastboot mode, your screen will read => FASTBOOT mode...

Open your instance of ADB and wait until the Auto Booter connects and puts your device onto the Fast Boot screen.

In your command/terminal instance, run fastboot flashing unlock

Next, press the Vol +Up key to unlock the bootloader

Now that your bootloader is unlocked, you need to run these commands

fastboot flash --disable-verity --disable-verification vbmeta vbmeta.bin

fastboot flash --disable-verity --disable-verification vbmeta_system vbmeta_system.bin

fastboot flash --disable-verity --disable-verification vbmeta_vendor vbmeta_vendor.bin

Now that you have access to the device fully, you will be able to flash the neutronscott images.
Run fastboot flash boot [your ns image].

run fastboot reboot

Done!

# Step 3 - Setup
Setup your device like normal

You need to re-enable debugging by running `*#*#33284*#*#`

For good measure, restart your phone.

Run `*#*#217703*#*#`

Run the magisk stub download

Restart your phone (again)

Update Magisk by hitting dpad down and hitting confirm.

Do a direct installation of Magisk through the app. When it says ramdisk yes you're good to go!! Congrats!

You are now totally done! You can stop here if you wish, or scroll below.

## Secret Codes
```
Enable adb: *#*#DEBUG#*#* (*#*#33284#*#*)

Launcher list all apps: *#*#217703#*#*

barometer calibration: *#*#1013#*#*

carrier choose: *#*#22384#*#*

testing settings *#*#73884647#*#* (Does something, not sure what)

Enable APN editing: *#*#9663223#*#*
```

## Settings
Enable PackageManager: resetprop -n ro.vendor.tct.endurance true

Enable virtual mouse (Without Magisk Module): settings put system keyboard_pointer_enable 1

Enable developer mode: settings put global development_settings_enabled 1

Allow hotspot: settings put global hotspot_entitlement_check_mode 0

Logging
Disable Write Protect: /vendor/bin/write_protect 0

dumpsys package log a on

dumpsys package log DEBUG_LOGGING on

dumpsys package log ENABLE_TRACE on

(I don't know what this is for, personally, but feel free to use it.

Creating the vMouse manually (Not Preferred) (credit to @NeutronScott)
Gflip6_TF:/ $ su

Gflip6_TF:/ # PATH=$(magisk --path)/.magisk/busybox:$PATH

Gflip6_TF:/ # mkdir -p /data/adb/modules/mymodule && cd $_

Gflip6_TF:/data/adb/modules/mymodule # vi module.prop

Gflip6_TF:/data/adb/modules/mymodule # mkdir -p system/usr/keylayout && cd $_

Gflip6_TF:/data/adb/modules/mymodule/system/usr/keylayout # cp /system/usr/keylayout/mtk-kpd.kl .

Gflip6_TF:/data/adb/modules/mymodule/system/usr/keylayout # cp /system/usr/keylayout/matrix-keypad.kl .

Gflip6_TF:/data/adb/modules/mymodule/system/usr/keylayout # vi matrix-keypad.kl

The contents of module.prop is described in the [Magisk Developer Guide](https://topjohnwu.github.io/Magisk/guides.html#moduleprop)

"I replaced key 138 FAVORITE_CONTACTS with key 138 FOCUS which disables the built-in function of the * key. (You can also change QUICK_DIAL in mtk-kpd.kl but I wouldn't touch the volume/power key!) Now that it does nothing we can assign it a function with an accessibility app."

### Important
# This stage installs the mouse as well as the App Store (Aurora store)

## Step 4 - Installing NeutronScott's vMouse 2/3
So, this is kinda necessary for almost every app but I keep it optional for yall. The easiest way to get the vMouse installed is to install it in magisk using a third party file browser. The phone's proprietary file manager doesn't see any modules, so using a third party one is the only thing you can do.



## Step 5 - Installing Aurora Store APK (Optional)
Run ./adb install [com.aurorastore].apk

You may either log into your google play account, or skip the login proccess.

Set your device to spoof
