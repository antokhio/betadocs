---
uid: a4d1962d-0a5b-4756-94b0-804b3317703b
---

# change log - vvvv50beta36
released on 20 03 18  

## VVVV
### general
* <a href="https://vvvv.org/blog/aspect-ratio-and-projection-space" class="extURL blog" target="_blank">aspect-ratio-and-projection-space</a>  
* fixed an issue where saving of patches failed and left ~temp files behind  
* when cloning from a c# or vl template dummy help and tags are now removed  
* CodeEditor: SaveAs now saves with correct file-extension  
* NodeBrowser tooltip now shows filenames  
* NodeBrowser deals correctly now with single-char tags  
* saving a patch to a new location now updates searchpaths  
* added link to "Tutorials & Demos" in main menu  
* setup.exe now checks for latest vs2017 redistributable  
* toggling UpdateView (CTRL+U) in patch is now visualized  
* replacing nodes with comments now works properly  
* CTRL+UP now works for all windows (not only patches)  
* added <a href="https://vvvv.org/blog/c6-compiler-for-dynamic-plugins" class="extURL blog" target="_blank">C#6 support for dynamic plugins</a>  
* closing the VL editor via CTRL+W now immediately asks for saving (not only when closing vvvv)  
* Fixed initialization issue when plugin was set multiple times during patch loading  
* Removed nupkg files from vvvv zip (reduced download size)  
* save all (alt-s) vs. save all + layout (ctrl-alt-s). now also ctrl-alt-s only saves patches that somehow got marked as dirty. Self (VVVV) node outputs layout changed info.  
* enum consuming nodes like Enum2Ord make sure to be aware of all user created enums. They also auto-evaluate to make sure that the enum reported to ioboxes upstream is up to date, even if the output might not be needed. New explicit versions of Enum2String, Enum2Ord, Ord2Enum and String2Enum now allow to adjust enum subtype with own configuration pin. Null node got legacy. CreateEnum now comes with a hidden input that allows to propagate the enum type upstream.  
* fixed resetting enums to default where default entry has a space inside.  
* regarding infamous "defaced IOBoxes" bug:  
  * patches now refresh after panning and when vvvv is deactivated  
  * added 2 commandline options: /refreshonf5 and /norefreshonscroll   
* NodeBrowsers ClonePanel now uses new directory chooser dialog  
* all nodes come with an Evaluate pin now; "Evaluate" pins are reserved to us and get red when created via plugin, hlsl or vl. They still should work. Added a test case for both assumptions  
* diffff mechanism now comes with /manualdiff option. see https://github.com/vvvv/vvvv-sdk/blob/develop/vvvv45/tests/testPack/manualdiff.xml for an example.  

###  plugin interface
* You now can write plugins that are aware of if they get evaluated or not. FrameDelay serves an example of how to make use of that feature.  
* tweaked mouse and keyboard .. notifications: sender is now attached to each notification. additionally VL got its own notifications, so they get converted on the way to VL.  
* the windows form Application.Idle event will now be raised by vvvv - useful to drive mainloops of other UI libraries  
* AllowFeedback attribute is obsolete. Implement IPluginFeedbackLoop to specify which ouput pins depend on which input pins.  
* Fixed deadlock when hitting breakpoint inside VS 2017  

### new nodes
* Line (EX9 2d)  
* Tokenizer (Raw), see: <a href="https://vvvv.org/blog/new-tokenizer-nodes" class="extURL blog" target="_blank">new-tokenizer-nodes</a>  
* BarcodeReader (String): decodes various 1d and 2d barcodes  
* Levin (2d/3d) (old ones are now set to legacy)  
* UploadImage DX9 and DX11 to send texture data from VL to the GPU <a href="https://vvvv.org/blog/vl-image-exchange-interface" class="extURL blog" target="_blank">vl-image-exchange-interface</a>  
* UploadBuffer DX11 to send generic data from VL to the GPU  

### fixed nodes
* CR, LF, CRLF (String) now have outputs  
* Gregorian (Split) now copes correctly with spread input  
* Fixed SetSlice nodes working with node pins  
* Fixed up/down events of special keys like TAB and ALT <a href="https://discourse.vvvv.org/t/keyboard-window-doesnt-like-tab/15636" class="extURL" target="_blank">https://discourse.vvvv.org/t/keyboard-window-doesnt-like-tab/15636</a>  
* GetSpread can now have negative offset  
* FirmataBoard (Devices): <a href="https://vvvv.org/blog/firmata-updates-and-fixes" class="extURL blog" target="_blank">decoder and I2C</a> are fixed. The node is now fully implemented in VL incl. serial communication.  
* Oscillator, Damper, Newton and LinearFilter now do not jump when reevaluated after some time.  
* SubDir and Dir auto evaluate <a href="https://discourse.vvvv.org/t/subdir-not-updating-unless-observed/15922" class="extURL" target="_blank">https://discourse.vvvv.org/t/subdir-not-updating-unless-observed/15922</a>  
* Texture (Split) help patch threw an exception on close  
* RelativePath now copes with basedirectories that have a trailingbackslash or not  
* Texture (EX9 Split)   
* Power (Value) now has better precision <a href="https://discourse.vvvv.org/t/power-node-bug/15950" class="extURL" target="_blank">https://discourse.vvvv.org/t/power-node-bug/15950</a>  

### changed nodes
* added Headers pin to HttpGet and HttpPost nodes  
* ArtNet nodes are now faster (powered by new UDP nodes in vl)  
* Date (Astronomy) is now ~10 times faster  
* Values can now be sent from a website to vvvv using window.vvvvSend function in the HTMLTexture node  
* changed the default for AspectRation (Transform).Alignment: FitIn -> FitOut  


## VL
### general
* <a href="https://vvvv.org/blog/vl-using-.net-libraries-and-writing-custom-nodes" class="extURL blog" target="_blank">vl-using-.net-libraries-and-writing-custom-nodes</a>  
* <a href="https://vvvv.org/blog/dynamic-dx11-buffers-in-vl" class="extURL blog" target="_blank">dynamic-dx11-buffers-in-vl</a>  
* <a href="https://vvvv.org/blog/vl-image-exchange-interface" class="extURL blog" target="_blank">vl-image-exchange-interface</a>  
* <a href="https://vvvv.org/blog/vl-one-frame-at-a-time" class="extURL blog" target="_blank">vl-one-frame-at-a-time</a>: better runtime exception and debugging support  
* node meta info (summary, remarks,..) now combines info from .xml with info saved in .vl document  
* PatchExplorer now updates correctly on UNDO  
* added hover style for comments  
* SaveAs in vl now references the newly saved file for its vvvv-nodes  
* use CTRL+2 to make a snapshot of a patch (also goes to clipboard)  
* toggle CTRL+4 to capture an animated gif of the current patch  
* tab history navigation now also via CTRL + < and CTRL + >  
* LineUp commands lines up patch elements: ALT+L  
* ALT+F1 searches for the nodes name on MSDN  
* Color IOBoxes now parse colors in different formats  
* values can now be edited on pins directly  
* the settings file is now only written when its content actually changed  
* pin tooltips now show values in more cases  
* indicator (top left of patch) now shows when compiler is preparing new build in the background  
* removed auto generated node definitions for enum entries - use IO box instead  
* the default value for a type can be defined with "CreateDefault" operation  
* value inspection will now also differentiate between the inner and outer parts of accumulators (all border control points for that matter)  
* do not mark unconnected pins in pin group as unused anymore  
* added Recompile command to context menu   
* synchronization of a patch with its symbol will now be done in background  
* links going into a region will now also act as seeds for the default moment inside the region.  
* the default value of an observable is now Never (instead of Empty) - that way one can nicely wait on values to come in. Needed for network nodes which pull in background  
* speed of patch tracing much improved by using a fixed sized array instead of concurrent dictionary to ask for a tracer  
* new region called Anonymous similar to Delegate primarily used by stateful lifting mechanism.  
* major rework of compiler which allowed us to write all primitive regions (Repeat, Foreach, If, Delegate, Anonymous) as plugins and put them into VL.CoreLib. This rework also exposed a couple of bugs related to apply pin and input group liftings.  
* improved support for interfaces  
  * once user adds an interface to class/record the interface will be implemented immediatly using default implementations  
  * implementing generic interfaces should work now  
  * defining interfaces should work now  
* Run, Stop, Pause modes added  
* new settings "RuntimePauseOnError" in combination with "RuntimeAutoJumpToError" to control wheter or not VL will stop executing nodes and jump to the node which triggered the last exception as well as "RuntimeDisableJITOptimizations" to make it more precise. The graph will also be colored based on whether a node was executed or not.  
* importing types, nested types, events to observable, forward all nodes etc.  
* Many many more little bug fixes and performance improvements  
* added easy base classes to write DynamicEnums  
* press CTRL+SHIFT+J to open .NET Dependencies in SolutioExplorer directly  
* Nested types show up correctly in SolutionExplorer  
* drag & drop types and nodes from the SolutionExplorer  
* reactive nodes throw their exceptions on the main loop for better debugging  
* dynamic enum switches to default entry un definition update when it was empty before  
* dynamic enums are sorted alphabetically, can opt out via property setter  
* added ManualDynamicEnumBase for dynamic enums that will be modified in VL patch  
* dynamic enum has a 'Tag' field to pass data along per entry  
* SolutionExplorer navigates to inport when a corresponding node clicked in patch  
* double click in vector editors works per component  
* patches can now be nested into each other  
* "Restructure Document" menu entry added. It reorganizes all patches by category and name.  
* node browser improvements:  
  * node browser allows to browse foreign symbols (nodes, types and categories) from assemblies and nugets. They get colored differently. This feature is only available when .NET nugets or dlls are directly referenced. For if this is distracting or too slow, you can temporarily hide those foreign symbols by clicking the button on the right of the search box.  
  * for when nodes are ambiguous, multiple choice questions for categories and pins pop up to select the exact overload. the followup choices concerning categories are displayed in a way that you can distinguish between the actual choice and the full category info (black versus grey)  
  * simplified logic when to show "Node" or "Region" choices: at the end of the decision process  
  * Primitives like ForEach get rendered in a special way and don't lead to further questions.  
  * Ok button now always closes node browser. Within the multiple choice browsing process a user can click OK at any time (most likely resulting in a red node, saying that it is somewhat ambigous. you can go back to the browsing process at any time by double clicking on the node)  
  * better tooltips  
* many compiler tests added  
* type inference improved  
* node and type references resolve/bind mechanism improved:  
  * now can deal with .NET type forwarding  
  * adaptive nodes: now version gets checked when still ambiguous. ToString (Hex) [[Adaptive] and alike now working  
  * improved performance of lookup algorithm.   
  * better tooltip for if node or type is not found: we now distinguish two infos: the "last dependency" and the "last file" the symbol was found in. The user now can see over which reference the symbol was found last, which should be easier to understand than where it was found.  
  * types get searched in extended scope (e.g. in all dlls that are somehow referenced by docs referenced by the current doc). By that type annotations in ioboxes are still resolveable. For nodes this is not done to keep the node browser clean.  
* cylcic graph checks improved  
* Edit->Expose Pins on a node creates inputs/outputs for all its pins  
* menu now shows documents red if they have missing dependencies  
* missing nugets can now be removed or installed via menu (if they are available on nuget.org)  
  * newly added nugets can be used right away without a restart.  
* new source package format PACKAGENAME/PACKAGENAME.vl   
* backup files now have the same relative paths than the original file  
* backup files now have the file extension .vlb  
* added shortcut Ctrl+Shift+I to copy GUID of currently selected element  
* reporting why very old files couldn't be loaded and how to work around  
* performance fix for enum pins on node with huge spreadcounts. Calculating error status of pin took to long.  
 
### fixes
* fixed laggy feeling on machines with high double click area in windows system settings   
* dynamic enums initialize correctly  
* improved resize cursor on regions and it shows correct arrows  
* allowing '_' for type annotations  
* debug timer will not call into native COM code anymore  
* time difference of IFrameClock will not be negative  
* renaming generic types also updates it's type annotations  
* importing enums sts them to immutable by default  
* double click while linking works in all regions  
* middle click while linking from any generic/adaptive/object input opens NodeBrowser with IOBox type choice  
* bool IOBoxes display bangs much better  
* regions with only pins as content have a min size  
* bang IOBoxes don't stop upstream values anymore  
* no more ToolTip flickers with wrong content  
* fixed jumps while dragging nodes caused by finished compilation from the background  
* fixed many redraw bugs after compilation is finished  
* improved alignment of CLR and VL symbol information so selection of which node to draw pink given a runtime exception should be better  
* got rid of a few special flags so replacing regions in a patch should behave better   
* added a safety mechanism to our serialization so ids are always unique which should allow the system to also load "broken" patches  
* fixed coloring of apply pins on process nodes  
* fixed Surround menu entry not creating full node reference so resulting region could be ambiguous.  
* fixed certain assemblies from GAC not showing up in reference dialog   
* fixed loading of GAC assemblies with dots in their name   
* fixed RAW input from vvvv to VL  
* couple of fixes regarding referenced documents:  
  * paths will be made absolute on deserialization and relative on serialization  
  * removed lookup magic of unresolvable VL documents through installed packages and added converter for old patches  
  * Fixed creating a new VL document if reference couldn't be found  
* couple of fixes related to imported and user written documentation of operations and pins not showing up in the node browser  
* fixed dummy types propagating in patches and should they appear in patches the tooltip will read "No type"   
* fixed empty sub patches being created on copy paste   
* fixed hot swap to run over all entry points at once and not individually for each of them.  
* in case there's no Update in a stateful higher order region one of the other subpatches will be chosen as default.  
* fixed vectors and colors being deserialized randomly   
* fixed links inside regions not being added to default patch   
* fixed type annotation on pads not getting picked up anymore after assign a slot to it.  
* changing the default category of a canvas wasn't picked up by incremental compilation.  
* fixed default value for IResourceProvider<T> by taking VL generated default resource into account.  
* fixed memory leak when using Spread<Resource<Stream>> as VL output in integration   
* fixed link assignments being lost after copy/paste   
* fixed error message complaining about recursive patches even though it wasn't recursive <a href="https://discourse.vvvv.org/t/vl-patch-window-freezes/15373/5" class="extURL" target="_blank">https://discourse.vvvv.org/t/vl-patch-window-freezes/15373/5</a>  
* "Input" and "Output" is a valid pin name now, system will use "State Input" / "State Output" in case of conflict  
* hot swap can now deal with multiple instantiations of the same type  
* links can no longer be made into an operation signature  
* fixed position of stream going into VL nodes not being reset   
* fixed importer treating input parameters as output parameters in case they had output marshalling information set  
* fixed move handler selecting a region from a different canvas as drop target   
* fixed state output showing up on process applications even though the kind of process was not explicitly set by the user  
* fixed assembly resolve issue in emitter which caused compiler to crash  
* default name for created pins while linking is now 'Input' or 'Output'  
* remarks in help text now also displays 'see' tags to other types or methods  

### new nodes
* \Cache [Primitive] region - will only execute if one of the inputs changes, the outputs will be cached  
* \SerialPort [IO]  
* \Tokenizer [IO]  
* \SplitToLines [String]  
* \SpreadMax [Collections]  
* \Delay [Animation], Delay (Linear) [Animation]  
* \GetValue, GetValues, GetVector2, GetVector3, GetVector4 [IO.OSC]  
* \GetValue, GetValues, [XML.XElement]  
* \XPathGetValue, XPathGetValues, [XML]  
* New UDP server/client implementation  
  * New type Datagram used by connection less networking nodes  
  * \New nodes Sender (Datagram) and Receiver (Datagram) - UdpClient/Server implemented with those   
* IPAddress and IPEndPoint have a proper = node now  
* Added a generic implementation for the != node to the VL.CoreLib  
* \Added DistinctUntilChanged [Reactive] and CombineLatest [Reactive]  
* C# scripting using Roslyn done with a new region called "Script" in VL.CoreLib.Experimental package  
* ToValues to convert vectors to spreads  
* Create (Sequence) to create a SpreadBuilder from any sequence  
* \Normalize [Path] to resolve any URI into an absolute path  
* Round (Digits) to round a value to the desired decimal places  
* IntPtr nodes to talk to low level libraries  
* \GetInternalArray [Spread] to access the underlaying spread data directly  
* fast mutable Builder classes for Dictionary and HashSet  
* adaptive constants like MinusTwo, MinusOne, MinusHalf, Half, Two...  
* Reactive nodes with Scheduler input to DevLib for better threading control  
* Triangle, Rectangle, Cosine and Sawtooth wave, also added comments and tagged all with "waveshaper"  
* CustomEqualityComparer to provide custom equality checks per type  
* Queue nodes  
* more Create nodes for Dictionary  
* KeyValuePair nodes to work with dictionaries  
* BufferDescription to send generic buffer data to the GPU via vvvv  
* Experimental WebSocketServer and simple HttpServer nodes  
* DMXUsbPro (Sender) node in new VL.Entec package  
* \OnOpen [Control]  
* Copy, Convert, Resize, ResizeAndConvert and Info nodes for Bitmap  
* BinarySearch versions for values, KeyValuePair and custom KeySelector delegate as well as Lerp versions  
* Combine for paths  

### changed nodes
* The patch inside of an if region can be stateful now - it can contain process nodes  
* \Improved speed of Reader/Writer [IO.Stream] nodes   
* TryParse and ToString are now adaptive  
* TryParse (Hex) nodes now can now also understand strings starting with "0x"  
* reactive nodes are a bit simpler and faster  
* animation nodes are faster because frame time gets cashed  
* Osciallator and Damper come with Cyclic pin  
* removed the nodes Control.Cache, Control.Cache (Experimental) and all IfAnyChanged nodes in favor of new Cache region  

### fixed nodes
* FileWatcher now calls its changed events on the main thread  
* \Fixed null pointer exception when using = [Object] and first input is null   
* Performance optimization in HTTPGet and HTTPPost nodes (affects vvvv also)  
* Got rid of the delegate hack in the Changed node. The observable wrappers now use proxies for delegate inputs so no check necessary.  
* Fixed default value of XDocument to also contain a root element so subsequent nodes don't crash with null pointer if a reader wasn't triggered yet.  
* Fixed AsyncTask and AsyncLoop not propagating inner exceptions and moved them from experimental to VL.CoreLib  
* MapWrap works correctly with negative inputs  
* added tags "applytransform" and "*" to vector transform nodes  
* Path nodes are much faster now  
* \Sequencer [Animation] now works properly and faster  
* fixed \ForEach [Reactive] regions randomly disposing the inner state while patching  
* fixed object disposed exception popping up when aborting the async task region in quick succession  
* fixed Zip node returning empty spread if one of its input counts was zero   
* \HoldLatest [Reactive] can be reset  

### girlpower
* 3D/CubeTree has better parametrization  
* added 2D/DifferentialGrowth  
* added DX/DynamicBuffersAndTextures  
* added Images/LoadAndSaveInBackground  
* added _Basics/ValueRecorder