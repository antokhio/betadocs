---
uid: 6b0c76ab-4edb-4508-b64a-a405add28435
---

# change log - vvvv45beta30
released on 22 05 13  

## general
* pressing F1 now opens a template helppatch when non is available  
* nodebrowser now allows filtering of whole categories  
* new shortcut: \ctrl+^ to jump to the parentpatch  
* start a link then ctrl+middle-click to create S/R accordingly  
* hold ALT while dragging a .v4p on a patch to make it an link instead of a subpatch  
* vvvv no longer crashes when having installed pd with its installer  
* fixed colors for drawing mainmenu and inspektor  
* architecture (x86/x64) now showing in splashscreen  
* ALT+E now also shows selected node in explorer (used to only open active patch)  
* ioboxes can now be autonamed by pressing SPACE+rightclick (alternative to middleclick)  
* rewrite of mouse and keyboard nodes. see <a href="https://vvvv.org/blog/update-to-mouse-keyboard-nodes" class="extURL blog" target="_blank">update-to-mouse-keyboard-nodes</a>  
* fixed range check error on startup in 64bit build on windows 8  
* CLR stack trace back in exception dialog and tty - got lost with unicorn upgrade  
* fixed various undo/redo issues  
* Artnet Port configurable via commandline argument /artnetport 6454  
* While Saving Patches: better workarounds for undeletable backup files. latest version will still have the userdefined name, not a cryptic ~temp name  
* fixed some memory leaks on ioboxes, geometry- & transform-nodes  
* boygrouping less chatty now. To get it even more mute just trigger <span class="pin">Enabled</span> of <span class="node">Boygroup (VVVV Server)</span> when you want to broadcast current bridges.  


* dynamic plugins  
  * code editor will now show warnings  
  * parsing of code files is now done lazily - will take longer until code editor comes up for the first time  
  * better logic whether or not a project needs to be recompiled (see <a href="https://discourse.vvvv.org/t/recompile-dynamic-plugins):" class="extURL forum" target="_blank">recompile-dynamic-plugins):</a>  
  * let a dynamic plugin be out of date if project's debug option doesn't match with assembly  
  * when comparing time stamps to decide whether or not a dynamic plugin needs to get recompiled take also a project's documents into account  
  * fixed an issue with plugins getting recompiled unnecessarily  
  * if a project's document doesn't exist create a "missing" document and show tool tip in project explorer - instead of crashing  
  * various smaller bug fixes regarding dynamic plugins and misconfigured project/assembly directories  

## new nodes
* PID (VVVV) returns the process ID of this running vvvv instance  
* Processors (VVVV) reports number of physical processors, processor cores and logical processors  
* Count (2D), Count (3D)  
* MonoFlop (Animation Framebased)  
* Encode (String Base64) and Decode (Raw Base64)  
* new RS232 (Devices) node - fully spreadable, uses data type RAW and outputs additional line states from serial port - see <a href="https://vvvv.org/blog/new-rs232-(devices)-node" class="extURL blog" target="_blank">new-rs232-(devices)-node</a>  

## fixed nodes
* Tidy (XML) fixed for unicorn  
* IOBOX (Value Advanced) no longer beeps when confirming a constant via pressing ENTER  
* Lumax (Devices) works again  
* Renderer (TTY) is autoscrolling again  
* fixed access violation in Intersect (EX9.Geometry Mesh) nodes  
* fixed memory leak in HTTP get/post nodes introduced from with new data type RAW  
* Enum2Ord (Enumerations) - some slices weren't evaluated correctly  
* OnOpen, OnActivate, OnQuit - validation issues fixed  
* Reader - validation issue fixed  
* OnResume - bug fix  
* LFO (Animation) - fix for LFO-Phase-Bug <a href="https://discourse.vvvv.org/t/lfo-phase-bug-when-starting-patch" class="extURL forum" target="_blank">lfo-phase-bug-when-starting-patch</a>  
* MP3Parser (File) reports data correctly again  
* all *ecue* nodes are working again  

## changed nodes
* SetPatch now has <span class="pin">Mark Patch as Changed</span>  
* IOBox (String) now has 'open' button in *Filename*, *Directory* and *URL* setting  
* GetElements (XML ByName) supports prefixed names now (prefix:name) and if no prefix given, will use default namespace of given XElement.  
* Mouse (Window/Global) output state of *XButton1* and *XButton2*  
* KeyMatch (String) node will also check for characters now (not keys only)  
* added new input pin "Validation" to AsElement (XML) node in order to enable DTD or Schema validation - by default validation is off, but in some cases (like parsing v4p files) validation is needed as the DTD file defines new entities  
* "Boygroup (Server) Enabled"-Pin only enables/disables bridge broadcast messages. other messages are always sent (e.g. patch messages)  
* added a Reset pin to simple filter nodes: <a href="https://discourse.vvvv.org/t/reset-pin-on-newton-damper-etc." class="extURL forum" target="_blank">reset-pin-on-newton-damper-etc.</a>  
* Prune (XML) is now named Prune (XElement) and supports generating text and children in addition to attribute output pins. Root element is now defined by XPath expression. Patches using the old version of Prune will need revision.  

## plugin interfaces
* renamed BufferedIOStream to MemoryIOStream - same naming scheme as .NET streams  
* new property IHDEHost.IsRunningInBackground  
* IOFactory can create in-place plugins now - for example look <a href="https://github.com/vvvv/vvvv-sdk/blob/develop/vvvv45/src/nodes/plugins/System/KeyboardNode.cs" class="extURL" target="_blank">here</a>  
* new interface IUserInputWindow which gets used by Mouse (System Window) in order to properly subclass a plugin's window  
* new property AllowFeedback on output plugin pins - see <a href="https://discourse.vvvv.org/t/dx11-feedback" class="extURL forum" target="_blank">dx11-feedback</a> for usage example  
* added basic support for future packs:  
  * add packs/PACKNAME/core to assembly search path  
  * add packs/PACKNAME/factories to mef container catalog on startup  
  * add packs/PACKNAME/nodes to node search path