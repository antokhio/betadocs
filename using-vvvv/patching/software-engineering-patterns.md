---
uid: 3eb927ab-9bda-4f94-8481-2cdc7ae67f0d
---

# Software Engineering Patterns

The following text is an updated transcript of the Workshop Software Engineering Patterns with vvvv at Node13 hosted by Sebastian Oschatz and Nils Buhlert.     


> You may also be interested in the <a href="https://github.com/vvvv/MoleculeViewer" class="extURL" target="_blank">material of the "Building Applications with vvvv" workshop</a> that applies some of the points made below to a demo project.  
  


![](~/img/vvvv-01.png "")   

The following list descibes some Patterns suitable to create maintainable and understandable patches with vvvv. Made out of long experience and from seeing vvvv patches growing from the well intended to the completely unmaintainable, it shows how to deal with bizarre change requests, insane deadlines, seemingly irreproducable interlocking soft- and hardware issues and any kind of disturbances covering all human senses .  

1. Six things in your mind 	
1. Scrolling is Slowwing
1. Separate Active from Passive Patches 
1. Passive Graphics
1. Global Graphics
1. Don't bake constants, don't bury relations
1. Flag Quick & Dirty (and come back)
1. Delay is for DebuggingDelay 
1. S&R with Care
1. One Patch per Role
1. Build a Wireframe
1. Use Versioning (e.g GIT)
1. The GIT Anomaly / The S&R advantage
1. Use the power of Pin Names 

Thanks to everybody attending the workshop and especially Sebl, Sunep and Zepi for reminding me about some more things, which i already included in this list.   

catweasel posted a rough video of the workshop - http://www.youtube.com/watch?v=NKAFhMjKnn8  

##  Six things in your mind 
 The brain has a particular limit on the number of things it can process at the same time. If you experiment e.g. with your ability to count different numbers of objects, you will notice that your brain will use different algorithms depending on the number of objects. For example small number of objects can be counted on the spot. Their fiveness or their threeness is instantly visible, no counting is necessary. With larger amounts of objects, counting needs to be done in the brain. There is no "seventeenness" - you will start counting from one to seventeen in your brain before you can know the number. If you want to count even more object you tend to get lost if not using your fingers or a pen to know where you are and where you have been. The time required for your brain is significantly different for all three algorithms. Seeing things on the spot is always the fastest way.   

###  What to Do
* Make sure that individual functions of your logic will have  maximum six functional clusters of nodes. While its possible to understand more things at once while being super-wake and super-alert, its more like 6 in normal state of consciousness. Lack of sleep, trade-fairs, press rehearsals, constant telephone calls, forklifts and electric power-tools will  reduce that count enormously and it can even go down to one or two   
* Learn to stop and don't waste time staring on things you cant mentally process.   
* Immediately start using tools (see below) or start refactoring. - use visual arrangement of nodes in vvvv to define clusters with independent functions   
* use the power of pin names (see below)   
* Refactor as often as possible, and use sub-patches, parent patches, Automata, Dynamic C#-Plugins etc. to find the most concise expression of your problem.   
* If you find a node for simplifying your algorithm, don't waste your time on NOT using it.   
* Always remove unused nodes and data paths in your patch. Use GIT to recover them later.   
* Remove logic for untested special cases   
* Remove premature optimizations for irrelevant situations   
* Strive for only  three to four functional clusters to have capacity in your brain to debug broken touchscreen power supply connectors, loose usb cables, flakey internet connections etc.  
* Practice Pair Programming:  2 Programmers fully alert will build excellent code right from the start.   2 supertired programmers with three things in their mind each will make (although painful)    
###  Why
* Debugging time will be multiplied by ten for each functional cluster of your patch which doesn't have the matching capacity in your brain to understand it.   
* You will need to work extra time to creating test environments, using pen- and paper, find someone to talk to, write TTY Renderer output etc. to fight against each cluster you cant intuitively catch in your brain.   
* Corollary: eight hours of sleeping can reduce debugging time from 10hours to six minutes.   
 

## Scrolling is Slowwing
* Patches can grow very big fast. A work space of infinite size can hold an infinite number of things. Note that you can see only a part of that infinite number of things at once.   
* Note that you can understand only six things at once.   
###  What to Do
* Make sure you can understand each cluster of nodes without scrolling.   
* Before you scroll, cluster your nodes. Often large patches can be made surprisingly small just by rearranging the nodes.   
* Before you scroll, maximize your windows. Tab Your Windows to be a able to switch between them easily.  
* Use big monitors.  
* Use the urge of wanting to scroll as a reminder of creating a subpatch. Use the urge to scroll in two dimension as a reminder of creating a subpatch RIGHT NOW ON THE SPOT.   
* If you have a long linear sequence of things going on (eg a large main patch with inputs, many processing steps and output)  scrolling may be actually faster than switching between patches.  Use lines (made out comments consisting of dashes) to separate different areas of the patch.   
###  Why
* if you start scrolling while patching a complex system you slow down your eye by orders of magnitude.  If you cant see everything at once, you cant understand everything at once. So better think of subpatches.    
* One  dimensional scrolling allows you to glance through the complete patch just by scrolling the mouse wheel. A patch which also extends in X direction needs to be searched in a zig zag or spiral pattern.  So scrolling in two dimensions makes finding  worse and might hide nodes at surprising locations.   
 

## Separate Active from Passive Patches 
There is a node category which is not really reflected in the Node menu: Active vs Passive Nodes.   
* the outputs of passive nodes are always fully defined by their inputs in the same frame (sometimes called pure functions or stateless nodes) .   
* The outputs of active nodes depend on the past  
Examples for active nodes are LFO, Damper, Automata, S+H, Flipflop, Framedelay and all nodes of the Animation category. Examples for passive nodes are Quad, Mouse,  +, Transform, RandomSpread, Renderer (if in redraw mode)   
Any active node will poison the whole patch active.   
###  What to Do
* Decide for a given patch whether it is an active or passive patch.  
* Active patches collect sequential logic – The  outputs depend on a previous sequence of steps, often by the user.   
* Passive patches are for abstracting things, eg. graphic layouts, sound engines, mathematical algorithms, external systems, render effects etc.  
* Avoid complex passive logic in active patches - always refactor to a sub-patch.  
###  Why
* Passive patches are quite straightforward to debug.   
* Passive patches tend to be more reusable, as the interfaces are more clear  
* Active patches are significantly more difficult to debug, as each debugging iteration needs time.    
* Active Patches need extreme mental concentration to observe temporal behavior. Temporal behavior is difficult to discuss.   
* Having simple, reliable and tested passive patches around you significantly reduces the amount of time for debugging the remaining active patches, as you can repurpose these for debugging purposes   
* Hidden states in passive patches create uncertainties whether all situations are observed and the test scenarios might be difficult to reproduce.   


## Passive Graphics
###  What to Do
* Avoid Dampers, LFOs, Monoflops, Automata in Passive Patches, especially in those creating visual output (near Shaders, Transforms, Spreads, Meshes, Render-passes etc.)   
* Control all animations from a parent patch.   
###  Why
* Graphics are quite simple to test while they are passive. Testing of animation effects is easy by manually scrolling through the animation from the parent patch, or connecting a simple LFO  
* Graphics tend to be quite node-intensive anyway, so separating as much as possible in a separate sub-patch creates two simple patches out of one big one.   
* Central Control of timing and speed  or Synchronization of effects in different sub-patches  gets easy.   
* Graphic modules get more generic and can be re-used quite simple  
* Graphic modules can be tweaked and refined by graphically inclined people or shader wizards without breaking existing logic.   


## Global Graphics 
###  What to Do
* Always have one global transform in a graphic patch, and base all further transforms in the patch on this.  
* Make sure to go the extra mile and also derive pixel precise billboards and typography from this global transformation.   
###  Why
* This the only way to reuse graphic modules   
* Adapting to different screen sizes is easy  
* Testing multi-monitor graphics on a one screen gets possible  
* Debugging graphic artifacts via VNC/TeamViewer gets possible  
* Hacking magnification modes to see details, pixel errors etc, on a small screen gets possible  


## Don't bake constants, don't bury relations 
Evaluating formulas directly in IOBoxes is cool but dangerous.   
We call the results of those calculations "baked" as you can not extract the individual numbers anymore  
###  What to Do
* Real Programmers only use -1, 0, 0.5, 1, 2    
* Each constant in your patch is a sign of weakness  
* π is for people not knowing about CircularSpread  
* 1 should be enough for everybody  
* If real programmers need other numbers, they calculate them using the Input values or Count.   
* Only Designers are allowed to use constants. Use constants only if they are the result of a deliberate design decision (e.g the size or color of an object). Note that beauty can change.     
* Never use constants to fit two independently patched things together (like aligning two objects together)   
* Always connect related spread-counts together, and always derive from some existing Count   
###  Why
* While its cool and simple in vvvv to change numbers to make things fit, they always bake results from unknown formulas or assumptions about other constants into your patch.   
* Baked Numbers hide connections, which will result in bugs when only one side is changed.   
* These dependencies exist only in the brain of the programmer and will be lost, when someone new takes over the patch. If made explicit you can simply SEE whats related.  
* So they create uncertainty whether a patch can be reused.    


## Flag Quick & Dirty (and come back) 
VVVV ist great for hacking quick prototypes, but take care to change to a different mode of programming when the prototype phase is over  
###  What to Do
* Always make a comment on quick hacks and explain the limitations.   
* Mark if something is not tested or somehow quirky   
###  Why
* it encourages people in the future to get rid of quirky code   
* a minute saved now will waste hours in the future   


## Delay is for DebuggingDelay 
Framedelay has two roles in vvvv.   
* The main Role is that to construct feedback loops to manipulate a state in a data flow language   
* The other role is to tweak things which are not working for whatever reason.   
###  What to Do
* Use FrameDelay to close feedback loops if you want to manipulate a state.  
* Resist the urge to fix things by adding a FrameDelay here and there. Use Renderer (TTY) with WriteLn to understand the exact sequence of things happening.  
* Even worse is the urge to fix thing with the time based Delay. Note that it is not guaranteed that a Delay will always need the same number of frames for time given in seconds.   
* If something is working, make sure to put into a well parametrized subpatch, test it and make sure you never need to change it again. So you never need to debug it again.   
###  Why
* VVVV is great because all things in a frame happen in the same time, which is great for debugging.  FrameDelay is tricky because things happening in the shortest possible time after another.    
* VVVV is great because you can just see things. FrameDelay makes it very difficult to just observe things. This will delay debugging.   


## S&R with Care 
S+R hides structure and relations  
###  What to Do
* Never Use S & R in passive patches, Use Inputs and Outputs in the patch and move the s&r to the containing active Patch.   
* Decide whether an active patch is "S&R clean" or not. Resist the temptation to use S or R in s&r-clean patches.   
* Define a small company wide set of global Receives which are okay (eg standard events for debugging, transforms etc).    
###  Why
* Debugging a patch which receives from many different patches will lead to having many different patches open at the same time.  
* S&R glue patches together - which makes individual reusable modules impossible   
* Patches containing S and R can only be reused in pairs.   


## One Patch per Role 
Complex projects have different stakeholders. There might be specialists for sound design, for lighting design, for various interfaces, for motion graphics etc.    
All stakeholders tend to change their system at different times, and are available only at specific times.   
The job of sub-patches is abstraction, in a sense that they encapsulate details which should only be changed when the system changes.   
###  What to Do
* Each Team member role will tell you about one particular aspect of the system  
* Write one patch per Team member role    
  * Sound Designer, File Names, Volumes, File Playback Parameters  
  * Light Designer, DMX Channels  
  * Media Integrator, Matrix Switcher Channels, Inputs  
  * Network Administrator, IP Addresses  
  * Device Vendor, Protocol Details  
  * Corporate Designer, Colors, Fonts, Backgrounds  
  * Motion Designer, File Names & Directories  
  * Mathematician, Complex Algorithms  
* Clearly state the team member role who provided the coded details in the patch.   
* Make sure each team member needs to open and change ONLY ONE patch. Make sure each patch needs to be edited by *only one* team member.  
* Build a debugging framework as a parent patch. Make sure the team member can use that framework to test its own subsystem.  
* Make sure that all other logic apart from the coded details is trivial, try to avoid active logic.   
### Why
* Only one person should be required to edit these patches and accidentally breaks something.   
* It is the only way to cleanly debug other people subsystems without being confused by your own errors (or errors of third persons which are not around)   
* It creates confidence and saves time for the other team members.   
* It creates a clean separation of responsibilities.   


## Build a Wireframe First

###  What to Do
* Try to find all required logic, modules and things  and bring them together   
* Setup patches for all  roles and think of who will fill in each part.  
* Create subpatches for all major logic components.    
* Do not waste time on details: Just create subpatches. Simplify logic of the subpatches to the max. Directly connect outputs to inputs. Use constants. Just use the subpatch to play with it in the parent.   
* Use placeholders for graphics. Use Text for displaying states and numbers. Leave out all graphic details, simulate all user input with the keyboard.  
* Start the implementation with the most difficult part, even if it will not impress the client.   
* Start with graphic patches only when the client starts wanting to "see" things  
### Why
* Find unknown problems early. You can't fix bugs in the concept with code.  
* Make sure to have all problems on the table to get a feeling of  the different parts of the application and their complexity, before deciding where to put the most resources in.   
* Use the prototype to explain the challenges to your team-members and split work accordingly  


## Use Versioning (e.g GIT)
If you go in the tedium of using Versioning, make sure you can enjoy the advantages.  
### What to Do
* Install the required software and learn how to use it.  
* If you go in the tedium of using a versioning system, make sure you can enjoy the advantages.  learn to revert, learn to understand the log files, learn to diff etc.   
* Be bold  
### Why
* This is the only way to change a running installation without breaking it.  
* This is the only way to understand a running installation without breaking it. (with vvvv reading is changing)  
* This is the only way to work in a team without getting insane.   
### Take Care
why is VVVV an Versioning sometimes so pain in  your ass:  
* Until now there are no usable visual diff tools  
* GIT is based on the the idea that merging is easy.  For now there is no vvvv merge tool.  So all the possibilities of branching are lost.   
 

##  The GIT Anomaly / The S&R advantage
Working with a team in the early stage of a project with vvvv and GIT creates an unique source of errors and frustrations. This is a subtle combination of features and lack of features:    
Imagine a root patch with many sub-patches. Two programmers work independently on individual sub-patches. The specifications are not completely fixed, so each programmer needs to introduce additional pins to their sub-patches and wire them in the parent patch. Often a programmer works on two subpatches and need to connect them at the parent level  
Note also that syncing the root without the sub patch will give inconsistent results for the other programmer.  As the vvvv/git combination allows no merge, this is bad.   
### What to do 
* Make sure to have all inputs and outputs rigorously defined before working on independent modules. This is classic 60ties top-down style.   
* Note that the problem can be significantly relieved by reducing the number of pins, which can be done by rising the number of Sends and Receives (see "S&R with Care")  So define a strict set of global variables for states, animation times, colors etc.   
* wish for a visual merge tool  
* wish for a deeply integrated and visual way of dealing with objects in vvvv   
* still dont hide S&R in the depth of supatches. Keep them on top of the first subpatch  


## Use the power of Pin Names 
### What to Do
* Use Modules with Inputs and Outputs whenever possible, as they provide a natural debugging technique.   
* Place named IOBoxes where ever possible in your patch.   
* If its impossible to find a name for something, think again of your algorithm.   
* Avoid using Stallone, Cons, Zip to collect unrelated data in one single connection whenever possible, as the names of the pins are lost at the other end. Its also quite tedious to fiddle with individual slices while debugging.   
###  Why 
* The time for discovering what a connection does multiplies extremely when there is no indication what it does.   
* Following a connection with your eye takes time. This time adds up, as it slows down thinking   
* Each indirection adds 1 to the number of things to have in your mind (see above)   
* Having an IOBox in place makes it simpler to change the value manually for testing. 