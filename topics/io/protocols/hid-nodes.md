---
uid: 5ac7763b-ae6b-48dc-b59b-85e1a601b1e8
---

# Introduction to Human Interface Devices (HID) in vvvv

HID is the name of a standard which is used to connect external devices to a personal computer. The HID standard was made with keyboards, game pads and button panels in mind, but is more and more common for all kind of gadgets, measurement devices or electronics development kits. It provides a simple-to-use bidirectional communication which is based on messages of a fixed length, the so called *reports*.  Devices are typically connected via USB. The HID specifies two channels, *Output* (which contains reports from the computer to the human) and *Input* (which contain reports from the computer to the human). Notice that the perspective is seen from the standpoint of the computer, so a thing typically considered as an *Input-Device* (like a game pad) will create *output* reports, and vice versa. For a device like a game pad a typical output report would for example contain the state of the controls.   

The basic operation of a HID in vvvv is very straightforward: Create a HID node, connect the *Input* and *Output* pins to some suitable string processing and set *Enabled* to True. In principle this works very similar to the TCP or RS232 nodes, they all establish a bidirectional communication based on strings. The HID specification includes some higher-level protocols, give some additional possibilities in vvvv.   

## Device Type List

As soon as an HID gets plugged into the computer it typically installs and saves its name from its internal ROM to the computer. So if you create a HID node and check the *Device Type* pin in the inspector, you will see a list of all currently connected HIDs. Note that many devices typically considered to be human interfaces are not technically HIDs – If the device does not show in the *Device Type* list, its probably no HID. For example most PS/2 devicesare technically not HIDs. Other devices may not have a proper name specified, so their name in the Device Type Pin in vvvv is composed of the unique Vendor- and Product-Id. Devices can register themselves more than once  

As you go through the devices on your machine, you will notice keyboard and Mouse HIDs. Unfortunately MS-Windows is configured in a way, that it automatically opens all installed Keyboard and Mouse devices *exclusively*. While this makes sense, as you can instantly *use* any Keyboard and Mouse instantaneously, it will at the same time disallows vvvv to connect to *any* mouse or keyboard node. Watch out for future features in vvvv.   

## Report Descriptors

A very distinctive feature of HIDs in comparison to older standards like RS232 is, that the devices themselves contain a *description* of the data packets they are communicating with - the so called *report descriptor*. Think of the Report Description as a miniature programming language which allows the developers of the devices to define a C-like struct which specifies how many packets the device supports, how large are the packets, and the purpose of each byte and bit in the packet. The programming language has a syntax simlar to an assembler language - its quite low level and not humanly readable. In vvvv you will deal with this language by means of long strings containing many hexadecimal characters.   

## Encoder and Decoder

Reports to and from a HID can be of multiple types, but each type has one fixed length of maximal 64bytes and a fixed syntax. Using the report descriptor from the HID node it is possible to automatically create encoders and decoders which will convert the input and output strings into their individual data parts. So using the HIDEncode and HIDDecode nodes in vvvv will save you from tedious patches with SpellValue, Ord and string operation nodes. The encoder converts numeric value pins into a string, which can be used as the input to a HID-node. The decoder converts the strings coming from the HID-node to simple to use value pins again. So if you want to connect e.g. a game pad, you would typically use a decoder, which converts the strings from the device into the X, Y, and button press informations.   

Sometimes for a game pad an encoder may also be useful, as some devices allow you to set various modes or parameters, or allow the control of LEDs or force feedback features on the device.  

To use the Encoder or Decoder nodes, these nodes need to be initialized with the proper report descriptor. To do so, check the HID-node with the Inspektor. You will see, that in the Output section it lists the report descriptor for each connected device. The report descriptor is a somehow long and scary string in hexadecimal notation, but it is not necessary to further understand its meaning – Thats what the Encoder and Decoder nodes are for. The report descriptor  gets directly read from the ROM of the device, and specifies which bit in the report is for what function.  To create a custom encoder or decoder, copy and paste that string (by means of the Inspektor) to the *Report Descriptor* pin of the HIDEncode or HIDDecode. As soon as you enter the string, new pins will appear in the HIDEncoder or HIDDecoder nodes. These pins now contain now exactly the parameters the hardware developers of the device wanted to expose for driver programmers. So a decoder feed with the report descriptor of a game pad will have output pins for X, Y axis, and various additional buttons and controls.   

## Report and Report Id

A device can send or receive different kinds of reports, identified by their Report ID. The You will find a list of all available ReportIDs of a device as output pins in the HID node. Encoders and decoders are always bound to a sepicific report id , which can be et as a configuration pin. A device might respond to different reports to allow sending different groups of parameters. Also devices do not always have to send all the data every time – the device might define different reports for different groups of controls. To deal with multiple output reports, connect multiple HIDDecode nodes to the Output Pin of the HID-Node, and set their ReportID.  The decoders will discard all reports which do not match the proper ReportID. Likewise only reports having a valid report id for the selected device will be accepted by the HID node.   

One note of caution: you will discover in practice that many hardware developers are a little sloppy in specifying the exact meaning of each bit, so a lot of guesswork or additional tweaking might be necessary. This is mainly because USB devices are not sold on the basis of the internal quality of the code basis of the drivers. Many hardware developers seem to be fine with the idea that only their colleagues in the software department need to understand how to write a driver and put very complex functionality in unnamed parameters or require complex settings to the device before it can be used.  But with properly designed HIDs, using the encoder and decoder nodes can be a huge time saver. If possible consult the documentation of your device.   

# Links

The <a href="http://www.soft-gems.net/index.php?option=com_content&task=view&id=14&Itemid=33" class="extURL" target="_blank">hid suite</a> by Robert Marquardt on which this vvvv component is based, contains useful applications to get   
information about the device or write/read reports.  

<a href="http://en.wikipedia.org/wiki/Human_interface_device" class="extURL" target="_blank">HID Wikipedia</a>  

The <a href="http://www.usb.org/developers/hidpage/dt2_4.zip" class="extURL" target="_blank">hid tool</a> gives the ability to create your own Report Descriptor  

Useful <a href="http://www.usb.org/developers/hidpage/" class="extURL" target="_blank">information</a> from the developers of the hid standard.  

<a href="http://www.usb.org/developers/devclass_docs/HID1_11.pdf" class="extURL" target="_blank">HID Specification</a>  

Book: USB Complete by Jan Axelson ISBN# 1-931448-02-7  

# Modules

<a href="http://www.vvvv.org/tiki-download_file.php?fileId=1901" class="extURL" target="_blank">meanimal.modules.HID</a>  

