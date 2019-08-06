# D̴̹̭͂ë̷̗́̃̿̓̾͜ṃ̸͔͚̗̙̪̎̄̋ȏ̸̝̤̱͜n̶͇͇͙̻̩͑͑S̴̳̩̮̥͚̥̚ė̸̟̃͋͂͝e̷̪̲̪̰̣̿̀͠d̵̡̂͗

.

DemonSeed is minimal malicious USB cable. Not to be confused with the O.MG Cable (https://o.mg.lol), which is a very differient piece of hardware that does a whole lot more, and is coming very soon :)

Table of Contents
=================

* [Intro](#-intro)
* [Materials](#-Materials)
* [Assembly Instructions](#-assembly-instructions)
  * [Board Assembly](#-board-assembly)
  * [Pogo Programmer Assembly](#-pogo-programmer-assembly)
  * [Cable Assembly](#-cable-assembly)
* [Programming Instructions](#-programming-instructions)
  * [Programming the Bootloader](#-programming-the-bootloader)
  * [Programming a Payload](#-programming-a-payload)
* [License](#-license)



## [↑](#table-of-contents) Intro
In 2017 I started playing around with miniaturizing HID attack hardware inside of USB cables. (https://mg.lol/blog/badusb-cables/) Since then, I have a lot of people request an easier way to reproduce this work, especially after someone ripped off the basic idea from private messages I sent them and started selling a modified version for hundreds of dollars. (hi kevin!) I don't think such a basic circuit is worth that much, but I do think it's a great way to learn about some hardware hacking basics by building your own. 

Yes, "DemonSeed" is another NIN reference :)

When assembled, these cables allow you to program a HID payload that is triggered on power up. The device plugged into the other end will receive power for charging. This makes for a decent educational demo. 



## [↑](#table-of-contents) Materials

This year (2019) at DEFCON I will have a bunch of these as build kits. So come find me! [https://twitter.com/\_MG_](https://twitter.com/_MG_)
In addition to the build kit, you will need some/all of the following depending on what level of build you choose:

* For Basic assembly:  
  * A soldering iron & solder
  * A sacrificial USB cable to implant into. These kits are designed to work with white lightning cables made by Apple, but any cable that fits inside the strain relief should work. 
  * Some Blu Tack/Mounting Putty will make soldering much easier. https://www.amazon.com/s?k=blu+tack

* For bootloader programming: 
  * Female to Female jumper/breadboard cables. 
    * Example: https://www.amazon.com/gp/product/B00R96X8JS/ 
  * An AVR ISP. 
    * There are a lot of options here. You can even make them out of Arduino capable devices, including other ATTiny's. If you don't want to figure this out, I have found the USBasp to be work with minimal work (works on OS X & Linux, need a driver for Windows). https://www.amazon.com/s?k=usbasp This specific one has worked just fine: https://www.amazon.com/gp/product/B00AX4WQ00/. **Just make sure to connect the J3 jumper or it won't work on the ATTiny85** 

* For assembly of the unpopulated PCB:
  * Solder Paste
  * A hot air reflow station, hot plate, reflow oven, a [spoon](https://twitter.com/_MG_/status/1152317329646088192) (not really), or any heat source that is appropriate for solder paste reflow.  

Don't have a build kit? Want to source your own parts? 
* per implant: 
  * PCB's created from the gerber files. 
  * 2x [DIODE ZENER 3.6V 150MW SSMINI2](https://www.digikey.com/product-detail/en/panasonic-electronic-components/DZ2S036M0L/DZ2S036M0LCT-ND/2269096) (most 3.6V Zener diodes under 500MW that have a SOD523/SSMINI2 footprint should work)
  * 2x [RES 68 OHM 1% 1/10W 0603](https://www.digikey.com/product-detail/en/stackpole-electronics-inc/RMCF0603FT68R0/RMCF0603FT68R0CT-ND/2418121) (any 68 ohm resistor with a 0603 footprint is fine)
  * 1x [RES SMD 1.5K OHM 1% 1/10W 0603](https://www.digikey.com/product-detail/en/yageo/RC0603FR-071K5L/311-1.50KHRCT-ND/729811) (any 1.5k ohm resistor with a 0603 footprint is fine)
  * 1x [IC MCU 8BIT 8KB FLASH 20QFN	](https://www.digikey.com/product-detail/en/microchip-technology/ATTINY85-20MU/ATTINY85-20MU-ND/1245919)
  * 1x USB connector + USB shell + flex relief. http://usb.makerusa.net is a recommended source for these. 
* per pogo programmer: 
  * 1x [CONN HEADER SMD 6POS 2.54MM](https://www.digikey.com/product-detail/en/amphenol-icc-fci/54202-G08-03/609-5602-ND/1488240)
  * 6x P75-E2 pogo pins: https://www.amazon.com/VDBX-io-Pogo-Pins-General-Use/dp/B07DJT5D6J
 



## [↑](#table-of-contents) Assembly Instructions
If you have a kit, then you have 2 boards that allow you to choose your own adventure here. 
**Full difficulty**: You can use the unassembled board and do 100% of the assembly. 
**Medium difficulty**: You can use the additional assembled board in the kit and skip to the pogo programmer assembly. 
**Easiest difficulty**: You can also use the same assembled board and skip directly to cable assembly because I preprogrammed all of these boards with a bootloader already. 

### [↑](#table-of-contents) Board Assembly
todo

### [↑](#table-of-contents) Pogo Programmer Assembly
todo

### [↑](#table-of-contents) Cable Assembly
todo


## [↑](#table-of-contents) Programming Instructions
There are two programming requirements. A blank ATTiny85 will need a bootloader flashed and the fuse bits set properly. After that, you can program HID payloads. 

### [↑](#table-of-contents) Programming the Bootloader
If you are using the board that came preassembled in a kit, you can technically skip this step be ause I flashed the bootloader already. However, it is still worth learning how to do this. If you have assembled the empty board with components, the ATTiny is empty so you will want to install a bootloader. 

First, install avr dude:https://learn.adafruit.com/usbtinyisp/avrdude

Then, download a copy of the ATTiny85 binary from the micronucleus project here: https://raw.githubusercontent.com/micronucleus/micronucleus/master/firmware/releases/t85_default.hex Micronucleus provides a really convenient functionality: It allows us to push payloads over a USB interface so we only need to use the pogo programmer once. 

Now, connect your ISP programmer to the 2x3 header on the pogo programmer using the jumper cables. **Please make note of the labeled pins. This 2x3 connector does not use a standard ISP pinout (sorry), so you need to ensure the proper pins are connected** Then press the pogo pins against the board. Two of the pads have small holes in the center that help the tips of the pogo pins click into place and keep them there. 

Verify connectivity by running `avrdude -c usbasp -p attiny85`

If connectivity is working, you can flash the bootloader and set the [fuse bits](http://eleccelerator.com/fusecalc/fusecalc.php?chip=attiny85) by running `avrdude -c usbasp -p attiny85 -U flash:w:t85_default.hex:i -U lfuse:w:0xe1:m -U hfuse:w:0xdd:m -U efuse:w:0xfe:m`


### [↑](#table-of-contents) Programming a payload
Install [Arduino IDE](https://www.arduino.cc/en/Main/Software) if you don't already have it.

If you don't already the DigiStump board manager installed, do so using [these instructions](http://digistump.com/wiki/digispark/tutorials/connecting). Then select board **DigiSpark (Default - 16.5mhz)** and select programmer **Micronucleus**. 

You can generate a payload script in a variety of ways. I recommend starting with a [DuckyScript](https://github.com/hak5darren/USB-Rubber-Ducky/wiki/Payloads) payload and then converting it with a [digiduck](https://github.com/uslurper/digiduck) which will output the entire Arduino sketch for you. 
Not sure which payload to try? Hak5 has a nice universal duckscript on their blog here: 
https://shop.hak5.org/blogs/news/what-is-the-best-security-awareness-payload-for-the-rubber-ducky

**LICENSE:**

These are intended for personal use and education in a nonprofit way. Please ask if you want utilize these for profit. 

![assembled](https://github.com/O-MG/DemonSeed/blob/master/display.png)
