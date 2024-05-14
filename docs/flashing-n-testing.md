# Testing and flashing instructions

After assemby your soldering kit you need to test the hardware. To do that you need to go through a simple checklist

1. Visual inspection - check that all components soldered good without unnesessary connections or short circuits with soldering drops. Check that all the boards clean from flux remains and other contamination.

2. Flash your Lisko flasher MCU (STM32) - instructions are [here](#How-to-flash-your-Lisko-board)

3. After that flash [kampela-solder-kit test firmware binary](../test-firmware/kampela-soldering-kit-test-firmware.bin) using [Pilkki software](https://github.com/Kalapaja/pilkki/tree/main/software) 

4. You can test everything except NFC power/data simply reconnecting USB cable. You should see several hardware tests on the screen with OK or ERROR results.

5. To test NFC power/data:

	- Disconnect USB cable
	- Turn on NFC on your smartphone
	- Put NFC-tag inside your assembled Kampela-soldering kit
	- Place Kampela with NFC-tag close to your smartphone's NFC antenna positions. You can find it googling in images or experimenting with NFC tag
	- If NFC power present - RED LED on Kampela should light bright. Keep this position.
	- In a couple of seconds the test firmware will start performing hardware tests showing results with OK or ERROR messages near each test

6. Now you can flash your Kampela with the latest kampela firmware release from here using [Pilkki software](https://github.com/Kalapaja/pilkki/tree/main/software)

7. You can find instruction of using your Kampela in [kampela-firmware repo](https://github.com/Kalapaja/kampela-firmware)

	Or make your own [kampela-firmware](https://github.com/Kalapaja/kampela-firmware)

## How to flash your Lisko board

First of all, you need to upload the flasher firmware:

0. Install STM32 DFU flashing software for example [stm32cubeprog](https://www.st.com/en/development-tools/stm32cubeprog.html)
	
	Or install alternative DFU software, for example dfu-util tool:
	
	On a Linux machine you can install it using:

	```
	sudo apt-get install dfu-util
	```
	
	for other systems, see http://dfu-util.sourceforge.net/

1. Hold RESET button and connect Lisko to your PC with a USB-C cable

2. STM32 flasher MCU will go to DFU mode and appear in your system as a DFU device. You can check its availability using:

	```
	dfu-util --list
	```
	You should see something like this:
	```
	dfu-util --list
	dfu-util 0.8

	Copyright 2005-2009 Weston Schmidt, Harald Welte and OpenMoko Inc.
	Copyright 2010-2014 Tormod Volden and Stefan Schmidt
	This program is Free Software and has ABSOLUTELY NO WARRANTY
	Please report bugs to dfu-util@lists.gnumonks.org

	Found DFU: [0483:df11] ver=2200, devnum=49, cfg=1, intf=0, alt=3, name="@Device Feature/0xFFFF0000/01*004 e", serial="315A35663432"
	```

3. Now you can flash the flasher by using:

	```
	dfu-util -a 0 --dfuse-address 0x08000000 -D pilkki_0.0.1.bin
	```

	from the folder, there pilkki_0.0.1.bin file was placed. By default, you can find it in [/flasher-firmware](flasher-firmware/) folder of this repository.

4. Perfect!

If you want to tinker with the flasher firmware, you can find the source code in [Pilkki repo](https://github.com/Kalapaja/pilkki/tree/main/firmware)

## How to program your Lisko board

Binary firmware can be uploaded to Lisko EFM32 MCU using [Pilkki software](https://github.com/Kalapaja/pilkki/tree/main/software)

You can find test projects here:

- In C - in [Lisko C test project](https://github.com/vasya-zh/Lisko/tree/A1/test-firmware)

- Or in Rust - [Kampela project](https://github.com/Kalapaja/kampela-firmware)
