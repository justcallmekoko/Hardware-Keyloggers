# Hardware-Keyloggers
Research done about modern hardware keyloggers

# Table of Constituents
- [Introduction](#introduction)
- [Hardware Keyloggers vs Software Keyloggers](#hardware-keyloggers-vs-software-keyloggers)

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

# Spachuhn's WiFi Keylogger
*This is only the beginning of the end.*
![This that thang](https://raw.githubusercontent.com/spacehuhn/wifi_keylogger/master/images/keylogger_with_nodemcu_2.jpg)
Spacehuhn's solution to the USB keylogger employs an ATMega32u4-MU in the form of an arduino 
