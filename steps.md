First off, you're going to need to enable ADB. That is done by entering *#*#33284#*#*. Once you have entered that and ADB is enabled, we can start the fastboot.

# Step 1 - Fastboot
Download the Pre-Reqs. . Download either neutronscott recovery, or magisk and insert it in the ADB Directory

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

You need to re-enable debugging by running `##33284##

For good measure, restart your phone.

Run *#*#217703*#*#

Run the magisk stub download

Restart your phone (again)

Update Magisk by hitting dpad down and hitting confirm.

Do a direct installation of Magisk through the app. When it says ramdisk yes you're good to go!! Congrats!

You are now totally done! You can stop here if you wish, or go to the next page.
