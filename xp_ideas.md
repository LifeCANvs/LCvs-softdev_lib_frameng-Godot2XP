## Ideas

This page is intended as a public dump of my thoughts and doesn't represent an obligatory to-do list.

- Implement multi-pass mode flag for FixedMaterial on GLES1 to get more accurate output to GLES2.
- Add some kind of "ScriptedMaterial" or fixed function shader system that works akin to Quake 3 shaders, for the GLES1 rasterizer.
- Look at the existing rooms/portals systems for salvagability. As far as I'm aware, it does not do anything useful and is completely broken.
Or I don't know how to use it. Could be either.
- Add icons for EventStream based resources like IT/XM/S3M/MOD files so it's more obvious what they're intended to be used with.
- Look into OpenGL 1.x extensions for adding features like framebuffer objects, so viewports render correctly.
- Make multi-texturing and vertex buffer objects optional features for GLES1 to lower the required OpenGL version, 
add feature caps emulation via project settings or editor viewport setting.
- I hate the way the Godot 2 FileSystem dock works and I really want the Godot 3 version.
- EventPlayer seems to be audio panned to the right, not sure why. Investigate this.
