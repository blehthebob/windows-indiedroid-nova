# windows-indiedroid-nova
Running Windows for ARM64 on the [Indiedroid Nova](https://indiedroid.us/) with a Rockchip RK3588S SoC, produced by ameriDroid, largely based on documentation for the [WoR Project](https://worproject.com/). The specific board we bought can be found [here](https://www.youyeetoo.com/products/youyeetoo-pico-pi-pc-rockchip-rk3588s-single-board-computer?VariantsId=11120).

Some of the files required for the installation below are included in this repository.

## How to set up Windows on an Indiedroid Nova board

### Disclaimer
This guide is based on our process and experience in setting up Windows for ARM64 on our Indiedroid Nova board. We are not affiliated with the WoR Project nor ameriDroid, and do not own any of the code mentioned in the below guide. We are not responsible for any possible damage that may occur on your devices through following this guide.

### Prerequisites
This is a guide for installation from a Windows computer. For Linux, see the WoR Project website [here](https://worproject.com/guides/how-to-install/on-rockchip#installation-from-a-linux-computer). Please note however that we have not tried this, and cannot comment on how well it is working.

* A1 SD card. We have found that only A1 (not A2!) rating SD cards work reliably when setting up Windows, so SD cards of any other type may cause errors in the setup.

* SSD drive. USB drives may also potentially work, however there is the possibility that they are too slow and will cause errors, so we heavily recommend using an SSD drive instead.

* eMMC (external MultiMediaCard). The Indiedroid Nova has an eMMC port, so these can be used as an alternative to the SSD drive. If you are planning on using eMMC, you will also require an eMMC to SD adapter which you can buy [here](https://www.okdo.com/p/emmc-to-microsd-adapter-board-for-rock-4c-rock-4se/?&campaignid=20180082399&adgroupid=&keyword=&matchtype=&creative=&network=x&device=c&product_partition_id=&product_id=2565012-gb&gad=1&gclid=CjwKCAjw5_GmBhBIEiwA5QSMxFdGhKlnHMOMXIhw8ln81StLm4NMUk4OyLimCLBinE8jbM4W5TRzhxoCtyYQAvD_BwE&gclsrc=aw.ds) or otherwise.

* USB-C power supply.

* HDMI to Micro-HDMI cable.

* USB-C dongle with multiple USB ports and an Ethernet port.

* Ethernet Cable.

* Necessary Peripherals, such as keyboard, mouse, etc.

* Monitor with an HDMI port.

### Preparing the Windows Image

The initial Windows ISO image can be downloaded using UUPDump:

1. Go to [https://uupdump.net/](https://uupdump.net/)

2. Under the Windows 11 drop-down list, select the "22H2" option.

3. Select a version of Windows 11 for the ARM64 processor. We have previously worked with builds v22621.1635, v22621.1928, v22621.2070, and know for certain that these versions should work, however there is nothing to suggest there may or may not be compatibility issues with other versions.

4. Choose the desired language for the system, and then click the "Next button". Then choose the desired edition of Windows - we worked primarily with Windows Pro. Then select "Next".

5. Ensure that the Download Method has been set to "Download and convert to ISO", and then Create Download Package. This will create a .zip file in the Downloads folder, which you can extract. For the time being, keep the files in the Download folder, otherwise this may cause issues during the download in the next step, due to the path name.

6. Open the extracted folder, and run the "uup_download_windows.cmd" file. This will open a command prompt window that will download the ISO image. This may take a while, depending on the quality of your internet connection. We have had situations from half an hour, to almost 2 hours in our experience. The download will have finished when the terminal prompts you to "Press the 0 key to exit".

7. After the download has finished, you will find multiple new files in the extracted folder. These include the .ISO windows image file, which should look something similar to: `22621.1.220506-1250.NI_RELEASE_CLIENTPRO_OEMRET_A64FRE_EN-GB.ISO`, though it may vary slightly depending on the build. This will be the Windows Image we are using in the next few steps. At this point in time, if you wish to, you may move the folder, or the image file into another folder that is easier to find if it is more convenient.

The image can be flashed onto and booted from either an SSD or an eMMC (external Multi-Media Card). We have worked with both, and therefore we have individual instructions below for each type of setup. In our experience, the eMMC tends to run faster than the SSD, meaning that perhaps it is more optimised for the eMMC. However, both options do work at very reasonable speeds, and there should be no issues regardless of which option is chosen.

#### &emsp;Image On SSD
1. Download the WoR (Windows on Raspberry) Imager from the WoR Project [downloads page](https://worproject.com/downloads#windows-on-raspberry-imager). It should download as a .zip file, which can then be extracted.

2. Plug the SSD drive you are intending to flash the image to, onto your computer.

3. In the extracted folder from step 1, you can run the `WoR.exe` file in order to run the WoR Imager.

4. On the first page, set the "Wizard mode" to "Show only the required options".

5. In the "Select the device" page, choose the correct drive from the drop-down list. You must ensure that the drive selected is correct, as this process will wipe the contents of the drive. Then for "Device type", select the "Raspberry Pi 2/3 \[ARM64\]" option.

6. On the "Select your Windows on ARM image", choose the .ISO file downloaded earlier, and select the correct Windows edition from the drop-down list.

7. Install the image onto the drive by clicking the "Install" option on the next page. The length of this process depends on the quality of internet connection, and may take upwards of an hour. However, once this is completed, the Indiedroid should be able to use the SSD as a boot-up device.



#### &emsp;Image On eMMC
1. Download the WoR (Windows on Raspberry) Imager from the WoR Project [downloads page](https://worproject.com/downloads#windows-on-raspberry-imager). It should download as a .zip file, which can then be extracted.

2. Download the eMMC driver [here](https://github.com/worproject/Rockchip-Windows-Drivers/releases/tag/v0.1) by downloading the production signed zip file under the 'Downloads' section.

3. Extract the dwcsdhc.zip file, double click on the dwcsdhc.cab file, then select all the files, right click them and click extract. Create a folder named 'drivers' and extract them into this folder.

4. Right click on this folder and click 'Compress to ZIP file'.

2. Mount the eMMC on the adapter, then plug this into your computer. If it is not recognised or will not fit into the SD card slot try plugging the adapter into a dongle.

3. In the extracted folder from step 1, you can run the `WoR.exe` file in order to run the WoR Imager.

4. On the first page, set the 'Wizard mode' to 'Show all the options'.

5. On the 'Select device' page select the eMMC, then for 'Device type' select the 'Raspberry Pi 2/3 \[ARM64\] option.

6. On the 'Select image' page, choose the .ISO file downloaded earlier, and select the correct Windows edition from the drop-down list.

7. On the 'Select driver' page, pick the 'Use a package stored on your computer' option and select the `drivers.zip` file you created earlier.

8. Select the default option on the 'UEFI firmware' page and click 'Next', 'Next' and 'Install'. The length of this process depends on the quality of internet connection, and may take upwards of an hour. However, once this is completed, the Indiedroid should be able to use the eMMC as a boot-up device.

### Flashing a UEFI on the board

We need to flash a UEFI firmware iamge to our board, so that it will behave almost like a regular desktop PC and will be able to boot.

Some boards come with NOR memory, which there are instructions for [here](https://worproject.com/guides/how-to-install/on-rockchip#preparing-the-board) on the WoR Project website, however we have not tried it, and cannot comment on how well it is working.

If you are using the Indiedroid Nova, there is no on-board NOR memory, so you will have to flash the UEFI to an SD card or eMMC(only if the Windows image is on SSD).

#### Flashing a UEFI to eMMC

1. Download an etcher tool, we used Balena Etcher: <https://etcher.balena.io/> (The following instructions will be for Balena Etcher).

2. Download the latest UEFI image for Indiedroid Nova: <https://github.com/edk2-porting/edk2-rk3588/actions/workflows/nightly.yml> Pick the latest successful nightly build and download the `indiedroid-nova UEFI Release image`, and extract the .zip file to get the UEFI image.

3. Mount the eMMC on the adapter, then plug this into your computer. If it is not recognised or will not fit into the SD card slot try plugging the adapter into a dongle.

4. Open Balena Etcher, select 'Flash from file' and select the UEFI image you just downloaded.

5. Select 'Select target', select your SD card and click the 'Flash!' button. You may need admin privileges to allow the app to make changes to your device

#### Flashing a UEFI to SD card

If you are using the Indiedroid Nova, there is no on-board NOR memory, so you will have to flash the UEFI to an SD card.

1. Download an etcher tool, we used Balena Etcher: <https://etcher.balena.io/> (The following instructions will be for Balena Etcher).

2. Download the latest UEFI image for Indiedroid Nova: <https://github.com/edk2-porting/edk2-rk3588/actions/workflows/nightly.yml> Pick the latest successful nightly build and download the `indiedroid-nova UEFI Release image`, and extract the .zip file to get the UEFI image.

3. Connect your SD card and open Balena Etcher.

4. Select 'Flash from file' and select the UEFI image you just downloaded.

5. Select 'Select target', select your SD card and click the 'Flash!' button. You may need admin privileges to allow the app to make changes to your device

### Startup

After preparing the boot-up drive (either the SSD drive or the eMMC), and the UEFI on the SD card, you should be ready to start up Windows on the Indiedroid.

1. Connect the Indiedroid board to the monitor via the HDMI to micro-HDMI cable, and connect the USB-C Dongle to the USB-C data port. The various USB peripherals and the Ethernet can then be connected to the board using the dongle, as well as the SSD if using the SSD to boot up. If you are instead using the eMMC, then attach the eMMC to the eMMC port at the bottom of the board.

2. Power on the board, by connecting the power supply to the USB-C power port. The board should now boot up, and the monitor will first display the ameriDroid loading page, and then the Windows set-up.

3. Windows will now take you through the rest of the installation process, and you can configure the OS.

## Troubleshooting

### Black screen on start

If you plug in the indiedroid after setup, and do not see the AmeriDroid loading screen, there may be a power issue. Sometimes, with the wrong power supply the board will not start - make sure that it is 5V/3A and if it still doesn't work just try other power supplies (we found that our power supplies did not all work consistently even though they were the same rating).

If the LED light on the board lights up but the screen is still black, there may be an issue with the UEFI. Remove the SD card and format it by deleting the UEFI volume in Disk Management (Windows) and reformatting the SD card. Then flash the most recent nightly build of the UEFI onto the SD card.

### BSOD

#### &emsp;On startup

You may have a USB stick left plugged in from the previous session. Unplug the power and remove the USB stick, then start the computer again and plug in the USB after it has booted.

#### &emsp;While running

This may be due to the GPU not working, anything that is graphically intense will not run well at all. We also found that this was more common with slower storage media so you can consider upgrading to faster storage. This is not a major problem, you should be able to unplug power and restart without worrying.

#### &emsp;On power off

This has happened to us occasionally although we don't know the cause. It has had no effects that we can see so far so you should be able to unplug power and restart without worrying.

### Inaccessible boot device

Your Windows image is probably on a USB stick or an SD card. This is too slow, so use an SSD or eMMC instead.

### UEFI doesn't recognise eMMC

You may have a USB stick left plugged in from the previous session. Unplug the power and remove the USB stick, then start the computer again and plug in the USB after it has booted.

You may have the wrong version of the UEFI. Download the most recent nightly build [here](https://github.com/edk2-porting/edk2-rk3588/actions/workflows/nightly.yml).

If this still does not work you may have the wrong eMMC driver. Follow the Windows flashing instructions again and make sure that you follow the instructions on downloading the driver as accurately as possible.

### No WiFi when setting up Windows

The Wifi is currently not working, but ethernet works if plugged in via a usb-c dongle in the board's usb-c port.

Another way to bypass this is by pressing shift-F10 to launch cmd, then type `oobe\bypassnro` in the command prompt and press enter. This will restart the computer and when you reach the "Let's connect you to a network" screen, click "I don't have internet", continue to click "limited setup", accept the license agreement and continue to create a local user account.

### Running slowly

This may be caused by Windows updating. Check the settings, and if Windows is updating let it finish the update. You can improve the speed by going to Settings > Accessibility > Visual Effects and turning off transparency and animation effects. You can also use the Windows + R shortcut to open the Run command, then type sysdm.cpl and pressing enter to launch system properties. Under "Performance" click the settings button, then select "Adjust for best performance" and click "ok".

If your computer is still running slowly look into getting a faster storage device for the Windows image.

### USB ports / Ethernet not working

USB 3.0 ports work, nothing else works except the USB-C port and micro-HDMI, so we recommend you use a USB-C hub to connect all your peripherals.

Note that the USB ports still work for power e.g. a fan, LEDs.