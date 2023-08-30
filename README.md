# windows-indiedroid-nova
Running Windows for ARM64 on the [Indiedroid Nova](https://indiedroid.us/) with a Rockchip RK3588S SoC, produced by ameriDroid, largely based on documentation for the [WoR Project](https://worproject.com/). The specific board we bought can be found [here](https://www.youyeetoo.com/products/youyeetoo-pico-pi-pc-rockchip-rk3588s-single-board-computer?VariantsId=11120).

Some of the files required for the installation below are included in the repository.

## How to set up Windows on an Indiedroid Nova board

### Disclaimer
This guide is based on our process and experience in setting up Windows for ARM64 on our Indiedroid Nova board. We are not affiliated with the WoR Project nor ameriDroid, and do not own any of the code mentioned in the below guide. We are not responsible for any possible damage that may occur on your devices through following this guide.

### Prerequisites
This is a guide for installation from a Windows computer. For Linux systems, see the [WoR Project website](https://worproject.com/guides/how-to-install/on-rockchip#installation-from-a-linux-computer). Please note that we have not tried this, and cannot comment on how well it is working.

* __A1 SD card__ - we found that only Class A1 (not A2!) SD cards work reliably when setting up Windows

* __SSD drive__ - USB drives may potentially work, but are much slower and can cause errors, so we heavily recommend using an SSD drive instead

* __eMMC__ can be used as an alternative to the SSD. If you are using eMMC, you will also need an eMMC to SD adapter which you can buy [here](https://www.okdo.com/p/emmc-to-microsd-adapter-board-for-rock-4c-rock-4se/?&campaignid=20180082399&adgroupid=&keyword=&matchtype=&creative=&network=x&device=c&product_partition_id=&product_id=2565012-gb&gad=1&gclid=CjwKCAjw5_GmBhBIEiwA5QSMxFdGhKlnHMOMXIhw8ln81StLm4NMUk4OyLimCLBinE8jbM4W5TRzhxoCtyYQAvD_BwE&gclsrc=aw.ds) or otherwise

* __USB-C power supply__

* __Micro-HDMI cable__

* __USB-C dongle__ with multiple USB ports and an Ethernet port.

* __Ethernet cable__

### Preparing the Windows Image

See the [WoR Project website](https://worproject.com/guides/getting-windows-images) for more details.

The initial Windows ISO image can be downloaded using UUPDump:

1. Go to <https://uupdump.net/>

2. Under the Windows 11 drop-down list, select the "22H2" option.

3. Select a version of Windows 11 for the ARM64 processor. We have worked with builds v22621.1635, v22621.1928, v22621.2070, so these versions should work. Newer and older versions may not be supported.

4. Choose the preferred language for the system and click "Next". Then choose the desired edition of Windows and click "Next".

5. Set the Download Method to "Download and convert to ISO", and then Create Download Package. This will create a .zip file in the Downloads folder, which you can extract. Keep the files in the Downloads folder for the next step, otherwise this may cause issues due to the path name.

6. Open the extracted folder and run the "uup_download_windows.cmd" file, which will open a command prompt window that downloads the ISO image. The download can take a while, depending on the quality of your internet connection.

7. After the download has finished, you will find multiple new files in the extracted folder. These include the .ISO Windows image file, which should look similar to: `22621.1.220506-1250.NI_RELEASE_CLIENTPRO_OEMRET_A64FRE_EN-GB.ISO`. This will be the Windows image we use in following steps.

The image can be flashed onto and booted from either an SSD or an eMMC. In our experience, the eMMC seems to run faster than the SSD, however, the difference is small and there should be no issues regardless of which option is chosen.

#### &emsp;Image on SSD
1. Download the WoR (Windows on Raspberry) Imager from the WoR Project [downloads page](https://worproject.com/downloads#windows-on-raspberry-imager) and extract the .zip file.

2. Plug the target SSD into your computer.

3. In the extracted folder from step 1, run the `WoR.exe` file in order to run the WoR Imager.

4. On the first page, set the Wizard mode to "Show only the required options" and click "Next".

5. Now choose the SSD from the drop-down list. Ensure that the correct drive is selected, as this process will wipe the contents of the drive. Then for Device type, select the "Raspberry Pi 2/3 \[ARM64\]" option.

6. On the next page, choose the .ISO file downloaded earlier and select the correct Windows edition from the drop-down list.

7. Next, flash the image onto the drive by clicking "Install" on the final page. The length of this process depends on the quality of internet connection, and may take up to an hour. Once this is completed, the Indiedroid Nova should be able to use the SSD as a boot-up device.

#### &emsp;Image on eMMC
1. Download the WoR (Windows on Raspberry) Imager from the WoR Project [downloads page](https://worproject.com/downloads#windows-on-raspberry-imager) and extract the .zip file.

2. Download the eMMC driver [here](https://github.com/worproject/Rockchip-Windows-Drivers/releases/tag/v0.1) by downloading the production signed zip file under the Downloads section.

3. Extract the dwcsdhc.zip file, double click on the dwcsdhc.cab file, then select all the files, right click them and click extract. Create a folder named "drivers" and extract them into this folder.

4. Right click on this folder and click "Compress to ZIP file".

5. Mount the eMMC on the adapter, then plug this into your computer. If it is not recognised or will not fit into the SD card slot, try plugging the adapter into a dongle.

6. In the extracted folder from step 1, run the `WoR.exe` file in order to run the WoR Imager.

7. On the first page, set the Wizard mode to "Show all the options" and click "Next".

8. Now choose the eMMC from the drop-down list. Ensure that the correct drive is selected, as this process will wipe the contents of the drive. Then for Device type, select the "Raspberry Pi 2/3 \[ARM64\]" option.

9. On the next page, choose the .ISO file downloaded earlier and select the correct Windows edition from the drop-down list.

10. On the Select drivers page, select the "Use a package stored on your computer" option and select the `drivers.zip` file you created earlier.

11. Select the default option on the UEFI firmware page and click "Next", "Next" and "Install". The length of this process depends on the quality of internet connection, and may take up to an hour. Once this is completed, the Indiedroid Nova should be able to use the eMMC as a boot-up device.

### Flashing a UEFI on the board

We need to flash a UEFI firmware image to our board, so that it will behave like a regular desktop PC and will be able to boot.

Some boards come with NOR memory, which there are instructions for on the [WoR Project website](https://worproject.com/guides/how-to-install/on-rockchip#preparing-the-board), however we have not tried it, and cannot comment on how well it is working.

If you are using the Indiedroid Nova, there is no on-board NOR memory, so you will have to flash the UEFI to either an SD card, or an eMMC if the Windows image is on SSD.

#### Flashing a UEFI to eMMC

1. Download an etcher tool. We used balenaEtcher: <https://etcher.balena.io/> which the following instructions also use.

2. Download the latest UEFI image for Indiedroid Nova [here](https://github.com/edk2-porting/edk2-rk3588/actions/workflows/nightly.yml). Pick the latest successful nightly build and download the `indiedroid-nova UEFI Release image`, and extract the .zip file to get the UEFI image.

3. Mount the eMMC on the adapter, then plug this into your computer. If it is not recognised or will not fit into the SD card slot try plugging the adapter into a dongle.

4. Open balenaEtcher, click "Flash from file" and select the UEFI image you just downloaded.

5. Click "Select target", select your SD card and click the "Flash!" button. You may need admin privileges to allow the app to make changes to your device.

#### Flashing a UEFI to SD card

If you are using the Indiedroid Nova, there is no on-board NOR memory, so you will have to flash the UEFI to an SD card.

1. Download an etcher tool. We used balenaEtcher: <https://etcher.balena.io/>, which the following instructions also use.

2. Download the latest UEFI image for Indiedroid Nova [here](https://github.com/edk2-porting/edk2-rk3588/actions/workflows/nightly.yml). Pick the latest successful nightly build and download the `indiedroid-nova UEFI Release image`, and extract the .zip file to get the UEFI image.

3. Plug in your SD card and open balenaEtcher.

4. Click "Flash from file" and select the UEFI image you just downloaded.

5. Click "Select target", select your SD card and click the "Flash!" button. You may need admin privileges to allow the app to make changes to your device.

### Startup

After preparing the boot-up drive, and the UEFI on the SD card, you should be ready to start up Windows on the Indiedroid Nova.

1. Connect the Indiedroid Nova to the monitor via the micro-HDMI cable, and connect the USB-C dongle to the USB-C data port. The various USB peripherals and the Ethernet can then be connected to the board using the dongle. Plug the SSD into one of the blue USB 3.0 ports on the board. If you are using the eMMC, attach the eMMC to the eMMC port on the bottom of the board.

2. Power on the board by connecting the power supply to the USB-C power port. The board should now boot up, and the monitor will first display the ameriDroid loading page, and then the Windows set-up.

3. Windows will now take you through the rest of the installation process, and you can configure the OS.

## Troubleshooting

### Black screen on start

If you plug the Indiedroid Nova to power after setup, and do not see the ameriDroid loading screen, there may be a power issue. Sometimes the board won't start due to an incorrect power supply - make sure that it is 5V/3A. If it is still not booting, try other power supplies. We found that the power supplies did not all work consistently, despite having the same rating.

More recent versions of the board have a LED light. If the LED light on the board lights up but the screen is still black, there may be an issue with the UEFI. Remove the SD card and reformat it by deleting the UEFI volume in Disk Management (Windows) and adding a new simple volume on the SD card. Then flash the most recent successful nightly build of the UEFI onto the SD card.

### BSOD

#### &emsp;On startup

You may have left a USB stick plugged in from the previous session. Unplug the power and remove the USB stick, then start the computer again and plug in the USB after it has booted.

#### &emsp;While running

This may be due to the lack of GPU support. Currently, anything that is graphically intense will not run well. We also found that this was more common with slower storage media, so you can consider upgrading to faster storage. This is not a major problem, you should be able to unplug power and restart without worrying.

#### &emsp;On power off

This has occurred occasionally, although we don't know the cause. It has no effects that we can see so far, so you should be able to unplug power and restart without worrying.

#### &emsp;Inaccessible boot device

Your Windows image is probably on a USB stick or an SD card. This is too slow, use an SSD or eMMC instead.

### UEFI doesn't recognise eMMC

You may have left a USB stick plugged in from the previous session. Unplug the power and remove the USB stick, then start the computer again and plug in the USB after it has booted.

You may have the wrong version of the UEFI. Download the most recent nightly build [here](https://github.com/edk2-porting/edk2-rk3588/actions/workflows/nightly.yml).

If this still does not work, you may have the wrong eMMC driver. Follow the Windows flashing instructions again, and make sure that you follow the instructions on downloading the driver as accurately as possible.

### No WiFi when setting up Windows

The Wifi is currently not working, but ethernet works if plugged in via a USB-C dongle in the board's USB-C data port.

Another way to bypass this is by pressing shift-F10 to launch the Command Prompt, then type `oobe\bypassnro`, and press enter. This will restart the computer. When you reach the "Let's connect you to a network" screen, click "I don't have internet", continue to click "limited setup". Accept the License Agreement and continue the Windows set-up process.

### Running slowly

This may be caused by Windows updating. Check the settings, and if Windows is updating let it finish the update. You can also improve the speed by going to Settings > Accessibility > Visual Effects and turning off transparency and animation effects. You can use the Windows + R shortcut to open the Run command, then type `sysdm.cpl`` and press enter to launch system properties. Under "Performance", click the settings button, and then select "Adjust for best performance" and click "OK".

If your computer is still running slowly look into getting a faster storage device for the Windows image.

### USB ports / Ethernet not working

USB 3.0 ports work, however nothing else is currently working except the USB-C port and micro-HDMI. We recommend you use a USB-C hub to connect all your peripherals.

Note that the USB ports still work for power e.g. fans, LEDs.
