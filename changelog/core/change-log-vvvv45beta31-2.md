---
uid: 3d93e8ec-24b2-44d2-ab2d-293d40a4a122
---

# change log - vvvv45beta31.2
released on 11 11 13  

## general
* SaveDialog now displays directory and filename in 2 lines  
* Jump2Parent patch now has international shortcut: ctrl+ the key below ESCAPE  
* tty now reports an error if a mididevice fails to open  
* Debug Spreads via Ctrl+F10  
* Alt+A now opens About patch (allows quick check of running version)  
* vvvv shouldn't block windows shutdown sequence anymore. See <a href="https://discourse.vvvv.org/t/vvvv-blocking-windows-7-shutdown" class="extURL forum" target="_blank">vvvv-blocking-windows-7-shutdown</a>  
* In case a node is missing write proper error message to the log and startup log  
* smaller memory footprint while patching  
* Much better dongle protection during runtime  

## boygrouping
* clients/server can again be started in any order and will find each other  
* clients again try to reconnect periodically when they lost connection  
* a memory leak that kept a copy of each graph-dump for each client is closed  

## new nodes
* Encode/Decode (String URL)  
* Encode/Decode (String HTML)  
* Encode (String HTML Attribute)  
* module Trigger (Animation)  
* module: Limiter (Animation)  
* Cons nodes in XElement Category  
* Vector swizzle nodes to convert between 2d and 3d vectors: xy, xz, yz, xyZ, xYz, Xyz  
* Skip (Raw), Take (Raw), GetBytes (Raw) and + (Raw Spectral)  
* complete spreadoperations for Raw category: Queue, Buffer, RingBuffer, SetSlice, DeleteSlice, Zip, Zip (Bin), Unzip, Unzip (Bin)  
* module: Randomize (Spreads)  
* module: IsActive (VVVV)  
* OnDeactivate (VVVV)  

## changed nodes
* MultiToggle (Animation) got an initialization option  
* Window (Windows) has its width/height pins no longer constrained  
* all midi nodes now default to Enabled=1  
* DMX (Network Artnet Sender/Receiver) now have their <span class="pin">SubnetID</span> and <span class="pin">UniverseID</span> correctly clamped to 15 and the <span class="pin">Do Send</span> is now single  

## fixed nodes
* Typospread: bugfixes and perforamce gain  
* MidiAllNotesOff now applies to all channels/notes correctly  
* Info (EX9.Texture) on x64 now correctly initializes sharedhandle to 0  
* Render (HTML Url/String) no longer throw javascript errors and now use IE10  
* Fixed issue in + (Raw) - read from first slices only.  
* Updated resource and memory management for Player (EX9.Texture):  
  * All players (in one node) share the same texture pool now  
  * Pools get managed per node (not node/slice like before)  
  * In each evaluate the player node will:  
  * Try to release unused pool memory - but will keep a little to avoid reallocation  
  * Release all unused textures  
* Vector join/split nodes are 4-5 times faster now  

## plugin interfaces
* API change: changed type of last parameter of IEffectHost.SetEffect to System.IO.Stream