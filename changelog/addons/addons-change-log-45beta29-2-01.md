---
uid: 9811ce82-7535-41a1-97dc-24c4f13e8a06
---

# addons change log 45beta29.2-01
released on 10 02 13  

## changed nodes
* Dialog (File Open) got bang output that indicates when OK button was pressed  
* Reader (File Advanced) now (String Advanced) with all encodings, and end of stream output  
* FirmataEncode (Devices 2.x) and FirmataDecode (Devices 2.x) data type changed from String to Raw, supports more than 16 digital pins, pin mode ANALOG implemented according to protocol specs, I2C decoding fixed + minor fixes and clean ups  
* Arduino (Devices StandardFirmata 2.x) reflects changes of Firmata plugins and thus adds support for all 20 pins as digital I/O, correct use of ANALOG pin mode  

## new nodes
* Dialog (File Save)  

## fixed nodes
* Store: no exceptions when trying to remove, set or increment on empty spread  
* Text (EX9.Texture): scaling outputs were delayed one frame  
* I2CDecode (Devices 2.x) works properly now, tested with hardware