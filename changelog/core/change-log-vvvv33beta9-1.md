---
uid: 6a347eca-5ca6-41f8-bce0-b377cb551255
---

# Change Log - vvvv33beta9.1
released on 16 11 05  
## general
* now shipping with beta5 opencv .dlls. freeframe plugins that use opencv need to be recompiled with those new dlls. did so with trautner and contours.  
* updated uninstall.exe to uninstall all .ax files in \bin  

## changed nodes:
* added a "Space" pin to DrawFixed and all old dx9 particles (Quad..) with which you can decide, in which space the particle is situated. when selecting "World" the particle behaves like before. if you don't want to interact with the camera (e.g. want to place a screen-aligned button you may want to place your Quad in "Projection" space. the view and projection transformations of the renderer won't infect this particle. if you select "View" only the projection of the renderer will infect your particle, cause it is already relative to the camera in viewspace..)  
* VertexBuffer (EX9.Geometry Join/Split) can work with 4d texture coords  
* Cylinder(EX9.Geometry)  has some more options  
* MainLoop's default time mode is 'raw' again  
* Toggle (Animation) added Reset pin   
* OSCDecoder (Network) deals with #bundles and outputs timestamp   
* WindowLists (Windows): removed some vvvv-internal windows from toplevel windows list  
* delay can be reset from now on  
* select nodes got a "Former Slice"-Pin  
* Contours (FreeFrame DShow9): added output 'Orientation' that gives a degree value for the orientation of each contour  
* freeframe plugins now handle r,g,b parameters as colorpin  
* various filenodes have their default filename mask changed from *.txt to *.*  

## new nodes
* Tidy (XML) Tidies bad HTML to proper XHTML  
* WavePlayer (DShow9) plays a spread of independent loops within one audio files.   
* HTTP (Network Server) serves Ressources via HTTP  
* HTTP (Network Receiver) receives HTTP-Requests  
* IsValid (XML)Validates XML against a DTD, returns if valid or not  
* IsWellFormed (XML) Checks whether XML is well formed or not  
* XPath (XML) You do a XPAth Query and it returns a Spread of Matches  
* XSLT (XML) transforms XML-Documents with XSL(T).   
* VideoOut (DShow9 DV) renders video directly to a dv-cam connected via firewire  
* PatchAlias (VVVV) Provides a link to a Parent Patch of a selected depth  
* Writer (EX9.Texture AVI) save textures connected to an AVI file  
* MidiTimeCode (Devices) get midi time code input   
* MidiClock (Devices) get midi clock input  
* GetPatch (VVVV) Returns the current XML-Description of a running Patch  
* Intersect (3d Quad Line) Intersection of a quad and a line  
* Intersect (3d Mesh Ray) Intersection of a mesh and a ray (directed line) the intersection nodes can be used to create buttons in 3d space  
* Delaunay (2d) minimized version of Delaunay (2d Triangle), outputs only the indices at one pin (consistent to mesh join)  
* * (3d Dot) 3-dimensional dot product  
* * (3d Cross) 3-dimensional cross product  
* Vector Join/Split for 2d and 4d  

## new modules
* Bone (Transform LookAt Vector).v4p   cool for inverse kinematics  
* Button (3d Quad).v4p   place Quads in space and be able to click them  
* InverseKinematics (3D 2Bone).v4p    the more coll for inverse kinematics  
* Light (EX9 Direction).v4p   display the light direct in the renderer and have easy access (pitch, yaw) to adjust the light direction  
* Light (EX9 Point).v4p   display the light position in the renderer  
* Normals (EX9).v4p   to display the normals of your mesh on your mesh  
* Projector (EX9).v4p   to create views on your virtual scene matching the real world scenario  


multiscreen:  
* MultiScreen (EX9 Dualview).v4p   use it to adjust 2 independent screens/renderers  
* MultiScreen (EX9 Spanmode).v4p   with this module you are able to ajust a grid of projectors with their overlaps and ajust the softgedge  
* ScreenNumber (EX9).v4p    display the number of a screen in the renderer)  

## bug fixes
* fixed a bug in the GlobalRenderState node  
* old particles like the Quad had a problem with textures on some machines  
* R nodes show only default value at the output pin but the correct values arrive  
* Switch (Value Output) outputs flickered  
* effects now accept #include files  
* videoplayback on kalles laptop (could have positive impact to other old graphic adapters/drivers too)  
* gray render bug (happened on older graphic adapters)  
* FileSource now deals with filenames > 128 characters  
* renderer didn't update backgroundcolor in attached dx9textures when hidden  
* device management debugged for complex scenes with feedback and many renderers.  
* fixed wrong interpretation of intersperse enum in +, qoute and separate(String)  
* fixed bug that sometimes caused a silent crash where everything was looking normal, but no patching/saving was possible anymore.  
* dualscreen IOBox click troubles fixed  
* the famous DPI settings bug is fixed. still 96dpi are recommended!  
* Writer (EX9.Geometry XFile): now deals with relative path filenames  
* VideoTexture Nodes: fixed bug that would not play videos on some graphic adapters, some switch-to-fullscreen bug fixed  
* Seperate (String) doesn't throw errors all the time  
* B-Spline had a small problem  
* Pipet (Texture) works correctly with spreaded textures  
* Dynamic Texture (Color), Dynamic Texture (Value) volumetexture bug fixed  
* Substitute (String). fixed that curious one.  
* Graph (Debug) had a small problem  
* some effects techniques had some problems with validation. if no texture is connected the default texture will be white  
* xfile writes more clear log messages  
* Perpsective (Transform OffCenter) fixed  