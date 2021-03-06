---
uid: 456e46ae-38dc-471a-94c8-b3914b79b51c
---

# Change Log - vvvv50beta37
released on 5th September 2018  

## VVVV
### general
* Much smaller download size  
* VL editor window is shown in task bar  
* Better startup time  
* improved document management: drop vl files onto vvvv patches or hit Ctrl-O to open them  
* added a "Show VL" command in main menu  
* setup.exe disables Win10 fullscreen optimizations by default  
* Fixed null pointer exception in texture marshaling code  
* Added MouseLostNotification so mouse states nodes can reset their state - see https://discourse.vvvv.org/t/mouse-device-mousestate-split-isnt-releasing-buttons-if-you-enable-or-disable-mouse/16440  
* Fixed regression mouse/keyboard state split nodes not working  - see https://discourse.vvvv.org/t/mouse-state-as-ouput-in-plugins-broken/16443  
* resetting color pins works again  
* richer tooltips for node pins  

### new nodes
* <a href="https://vvvv.org/blog/htmltexture-now-for-dx11-and-more" class="extURL blog" target="_blank">HTMLTexture now for both DX11 and DX9</a>  
* AsImage (DX11.Texture2D) to move a dx11-texture over to vl-image land  
* Processes (Windows Async)  

### fixed nodes
* Tokenizers now handle irregular input correctly  
* Camera (Orbit) hast damping again  
* Fixed division by zero in Text [EX9] node when fed with nil  
* AsImage node will turn red in case it can't handle the incoming texture instead of just logging to tty  
* Disabled context menu in HTML texture  
* fixed small issues on CreateEnum (no multiline string, rare cyclic patch involving this node now works)  
* Ex9 renderer with clear turned off: when re-enabling the renderer we now don't clear it  

## VL
* big <a href="https://vvvv.org/blog/vl-corelib-cleanup" class="extURL blog" target="_blank">CoreLib Cleanup</a>   
  * introducing keywords "Experimental", "Advanced", "Obsolete"  
  * "Internal" to hide nodes  
  * Adaptive nodes now can spread into different categories  
  * many NodeBrowser refinements  
* Tooltip and Nodebrowser not always on top  
* <a href="https://vvvv.org/blog/vl-improved-file-io" class="extURL blog" target="_blank">Improved File IO</a>  
* <a href="https://vvvv.org/blog/vl-patch-your-own-mainloops" class="extURL blog" target="_blank">Patch Your Own MainLoops</a>  
* <a href="https://vvvv.org/blog/vl-serialization" class="extURL blog" target="_blank">Better serialization</a>  
* <a href="https://vvvv.org/blog/vl-groups-and-categories" class="extURL blog" target="_blank">Groups and Categories</a>  
  * groups now can be placed everywhere  
* Frames  
* Fix for undo/redo where sometimes the wrong patch got tackled  
  * note: a name change of a type, group or category is always covered by the undo history of this element. For undo you need to navigate into it.  
* Better exception reporting  
* improved document management:   
  * Close a document via Ctrl-F4  
  * Ctrl-W closes a tab. Hiding last tab hides window  
  * Drag dropping VL documents now simply opens the document as this is 99% of time what you want  
* added scrollbar for enum dropdowns  
* fixed glitches for enum dropdowns  
* less verbose warning for mutable links (now only visualized with a yellow sock at the end of a link)  
* IOBoxes cannot be interacted with anymore if only used for display  
* SolutionExplorer navigates to open patch when opened  
* Cache region can optionally dispose cached objects when creating new ones  
* added many help texts to nodes  
* dynamic enum for installed system fonts  
* color editor remembers hue and saturation while changing value with mouse  
* Destroy operation is now called Dispose as in .NET  
* tooltip now uses custom ToString method (if defined) to display values  
* In case hot swap fails the exception will be logged and the runtime will be put into the stopped mode so user can act upon error accordingly   
* Rewrote how incremental compilation works and how model gets synchronized to symbols  
  * Compiling should be quicker now  
  * Fixes issues like "Object is no subtype of Object" when patching in document referenced by others   
  * Fixed that the UI wasn't always in sync with current compilation  
* Enabled pin groups on process nodes   
* Do not generate unique names anymore when pasting elements   
* Added support for multi dimensional arrays   
* Destroy is now called Dispose and user has to implement IDisposable interface on patch explicitly  
* Added non-generic ISpread and ISpreadBuilder interfaces  
* Added IVLObject interface which gives access to the VL runtime graph in a nice dynamic fashion  
* Added IVLTypeInfo and IVLPropertyInfo in order to be able to reflect on VL object graph   
* Added IVLFactory interface which gets passed in to new static RegisterServices entry points  
* In case a VL document defines a non-generic RegisterServices operation it will be called once after each re-compile. For many documents they will be called in reverse topological order  
* Virtual methods of the Object class can now be overriden (ToString, Equals, GetHashCode)  
* Whether emitted VL types behave in an immutable fashion is now decided by an internal flag -> process nodes can be mutable as long as the surrounding context is  
* Loops will now re-use the output spreads and only create new ones if the data actually changes   
* Hot swapper will now traverse deep into the VL graph in order to figure out whether or not a swap is needed   
* Removed restriction for apply pin lifting that first pins must be named Input and Output   
* Documents can now be reloaded from disk  
* Color editor remembers hue and saturation while dragging  
* Redo now also works with CTRL+Y shortcut  
* Splash screen for first long VL compile  
* library developers can use the "lib-native" pattern early on. freeing them from the need of creating a package before they even start working on the library  
* IOBoxes have much less annoying tooltip  

### new nodes
* Spread generator nodes (LinearSpread,...) are now Processes with their stateless companions (CreateLinearSpread,...) being marked as advanced  
* HoldLatestError (Reactive)  
* MultimediaTimer and BusyWaitTimer see <a href="https://vvvv.org/blog/vl-patch-your-own-mainloops" class="extURL blog" target="_blank">vl-patch-your-own-mainloops</a>  
* MidiClock in/out  
* MidiMonitor to debug midi messages  
* MidiPlayer to play back midi files  
* Rectangle creators with anchor point  
* Scale and Inflate to modify rectangles in each direction  
* RotateBetween to rotate objects from one direction to another direction  
* AlignBetween to align objects between two points  
* TryDispose to safely dispose objects and collections  
* Four new experimental nodes called TryGetValue, TryGetValueByPath, WithValue and WithValueByPath which allow you to modify VL instances in a rather dynamic fasion  
* FromImage [Bitmap]  
* Imported all mutable .NET collections like List, Dictionary, HashSet...  

### fixed nodes
* Filename (Split) has now string as first output to be opposite of Filename (Join)  
* MidiOut closes device properly  
* Filter (Animation) has a "Reset" pin  
* OnOpen has a "Simulate" pin  
* Fixed AsyncLoop stopping when patching outside of it   

### changed nodes
* Serial port sender and datagram sender nodes will now turn pink if they catch exceptions on background thread  

### bug fixes
* Fixed region choice not showing up on directly imported nodes   
* Fixed default values not being copied to pin group pins   
* Fixed not being able to get rid of red apply pin   
* Fixed invalid target code when passing struct to method expecting an interfaces - boxing was missing  
* Fixed dead lock when debugging with Visual Studio 2017  
* Fixed issue where ForEach region was broken after Copy&Paste  
* Border control points outside of regions will now show proper error message and will be rendered by UI  
* Fixed Ctrl+Plus adding pins on nodes where lifting is not even supported - see https://discourse.vvvv.org/t/adding-pins-to-generic-fails/16348  
* Fixed image copying functions to take scan size into account  
* Fixed super expensive equality check of Path  
* Fixed broken links when moving a selection into operation definition   
* Fixed stack overflow when creating and using a custom operation called "With" on a class or record   
* In case hot swap crashes for a particular field create the whole value anew  
* Fixed pin value of optional apply pins on process nodes not working  
* Fixed issue in converter of old VL patches that Break or Keep pins inside loops didn't show up anymore  
* Fixed custom value indicator not working on first pin in case by-pass lifting was applied  
* Fixed some settings not being reloaded when saving settings file   
* Fixed crash when installing a package while vvvv/VL is running   
* Fixed performance issue in compiler when opening patches with many links  
* Fixed performance bottleneck in UI code when looking at patches with many links and subpatches  
* Fixed a dead lock when loading VL documents  
* Fixed a crash in "Code" window 