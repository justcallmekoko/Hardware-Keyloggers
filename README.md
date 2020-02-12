# Hardware Keyloggers
Research done about modern hardware keyloggers

# Table of Constituents
- [Introduction](#introduction)
- [Hardware Keyloggers vs Software Keyloggers](#hardware-keyloggers-vs-software-keyloggers)
- [Spacehuhn WiFi Keylogger](#spacehuhn-wifi-keylogger)
- [Maltronics WiFi Keylogger](#maltronics-wifi-keylogger)

# Introduction
Hardware keyloggers serve as an alternative to software keyloggers. They are typically places in-line between a USB keyboard and a victim computer whether it be installed directly in the keyboard itself of sitting between the Male USB plug of the keyboard and the Female USB port of the computer. I have been googling my ass off for a while now looking at datasheets and forum posts trying to gather as much information I can about hardware keyloggers. I want to compile all of the information I can about this subject and place it here for anyone else who is interested. I have been developing and will continue to develop POCs for hardware keyloggers and I will post the information here.

# Hardware Keyloggers vs Software Keyloggers
To be honest, I am starting from scratch here. Relative to what there is to know about hardware keyloggers, complex microcontrollers, and the USB protocol in general, I know nothing. I have written software based keyloggers in the past. Some have been very awful and stay top level and others have been decent and use keyboard hooks. Software based keyloggers have their advantages and disadvantages.  
**Software Keylogger Advantages**
- Physically undetectable (no physical presence)
- Victim keyboard functions as normal
- No physical access required for installation or exfil
- No hardware resources required
- Functionality not limited by space (unless you care about file size)  

**Software Keylogger Disadvantages**
- Detectable by antivirus
- Only logs keys after OS loads
- Uses computer resources  

I am really good at spelling and going down rabbit holes. I found out about hardware keyloggers when I went looking for alternate solutions. At first I saw [Spacehuhn's](https://github.com/spacehuhn) [wifi keylogger](https://github.com/spacehuhn/wifi_keylogger) project and I was impressed. It was able to log keys and display them over WiFi via web browser. It has it's disadvantages which I will detail in specifics later. This was my first introduction to the concept of hardware keyloggers and I was hooked. No hardware keylogger is created equal, but they do have inherent advantages and disadvantages.  
**Hardware Keylogger Advantages**
- Starts logging keys before OS Loads
- Undetectable by antivirus
- Does not use computer resources (other than power)  

**Hardware Keylogger Disadvantages**
- Physically detectable
- USB Keyboard data can be misinterpreted and in some cases can causes missed keys on the computer
- Requires physical access to victim computer to install
- Microcontrollers and programming hardware required
- Functionality limited by space  

# Spachuhn WiFi Keylogger
*This is only the beginning of the end.*
![This that thang](https://github.com/justcallmekoko/Hardware-Keyloggers/blob/master/Images/keylogger_with_nodemcu_2.jpg?raw=true)
Spacehuhn's solution to the USB keylogger employs an ATMega32u4-MU in the form of an Arduino Leonardo, an Arduino R3 style [USB Host Shield](https://www.amazon.com/SainSmart-Android-Arduino-Mega2560-Duemilanove/dp/B006J4G000), and an ESP8266. This keylogger accomplishes what all hardware keylogger need to accomplish to a point. It falls victims to the shortcomings of the [Keyboard library](https://github.com/arduino-libraries/Keyboard) and the behavior of the USB Host Shield in that some keys typed on the keyboard are not able to be translated properly and therefore do not pass on to the host computer. This would cause concern for any victim typing on their computer when they see characters that don't align with what they typed or no characters at all. For those who are comfortable working with Arduino but have not gotten into ARM or CPLD/FPGA microcontrollers yet, I recommend this project. You learn a little bit about WiFi, keyboard emulation, and the USB protocol.  
## How It Works
The ATmega32u4-MU is incapable of hosting a USB device. It's functionality *as* a USB device is what makes it a valuable part of this setup. It's inability to host USB devices is compensated by the USB Host Shield which uses a [MAX3421EE](https://www.mouser.com/Datasheets/_/?Keyword=MAX3421EE&FS=True) USB host controller to host the USB keyboard. The MAX3421EE is able to take the USB data from the USB keyboard an pass it onto the ATmega32u4-MU via the [SPI bus](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface). These keypresses are passed to the ATmega32u4 which "replays" them to the host computer using the Keyboard library. While these key presses are being relayed, all presses passed by the ATmega32u4 are additionally passed to the ESP8266 which logs the keys in flash memory and displays them on a web page. This web page can be accessed by connection to its hosted WiFi access point and navigating to `http://192.168.4.1`.

```
[KEYBOARD] -----> [MAX3421EE] -> [ATMEGA32U4] -----> [COMPUTER]
                                      |
                                      |
                                      V
                                  [ESP8266]
```
The next trick is to figure out how to place all of these components onto one small board. I have searched the internet to see if anyone has made an attempt at designing a custom PCB for this project and I have not found one. 


# KEYVILBOARD
*Fast boats and even faster hoes*

## How It Works
*idfk*

# Maltronics WiFi Keylogger
*Somebody stop me!*
![God hates us](https://github.com/justcallmekoko/Hardware-Keyloggers/blob/master/Images/unsheathed_mini.JPG?raw=true)
So I am still trying to figure out how this keylogger works. This is where it gets a little complicated for those who have not worked with CPLD/FPGA style microcontrollers. I fall under this category as I do not understand these myself. These microcontrollers are a bit outside of the relm of Arduino and we get into the world of JTAG and assembly. Unfortunately for the functionality we want, these microcontrollers seem to be the widely accepted solution among dime-a-dozen Chinese manufacturers. 

<p align="center">
  <img alt="Librarian" src="https://github.com/justcallmekoko/Hardware-Keyloggers/blob/master/Images/5m160ze64c5n.JPG?raw=true" width="400">
  <img alt="Librarian" src="https://github.com/justcallmekoko/Hardware-Keyloggers/blob/master/Images/esp8266.JPG?raw=true" width="400">
</p>

These microcontrollers may be complicated, but they still manage to pack a very tight footprint. I had to dawn every macro extension I had for my DSLR in order to photograph the vendor markings on the cap of the main chip.
<p>
  <img alt="Librarian" src="https://github.com/justcallmekoko/Hardware-Keyloggers/blob/master/Images/macro_lenses.jpg?raw=true" width="300">
</p>

### Important Components
- Intel Altera 5M160ZE64C5N: CPLD microcontroller
- Epsressif ESP8266EX: WiFi enabled microncontroller
- winbond 25q128jv: Serial flash memory

## How It Works
*No Idea*
