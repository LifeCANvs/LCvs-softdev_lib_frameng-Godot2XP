## Godot 2 XP - What is this?

Godot 2 XP is a fork of Godot 2.1.7 RC that not only runs on Windows XP,
but it implements a fixed-function OpenGL 1.x compatible rasterizer for lower tier PC GPUs.
I made this because I have a crappy Windows XP computer that I like to tinker with.
This functionality could be ported to other low-tier platforms, but I am only a Windows user.

This version of Godot is not intended as a drop-in replacement for Godot 2 games, and is an enthusiast version made for my own purposes.
I may add new features not present in the original Godot 2.1 version intended for my own use.

#### Can I use this to load existing games?

The GLES1 rasterizer ported from Godot 1.0 has fundamental differences from the GLES2 rasterizer.
Existing games made for Godot 2 target the GLES2 renderer, but this fork uses the GLES1 renderer by default for compatibility reasons.
If you try loading a GD2 project in this, it might not look correct without tweaking the video driver setting.

#### Why should I use this over modern Godot?

You shouldn't. This fork isn't intended to replace modern Godot versions.
If you're looking to make a retro style video game, you can probably do that just fine with any newer engine.
If you're the retro PC enthusiast type that's willing to put up with an old version of Godot despite its quirks, 
because you want your game to run on hardware it looks like it should, this version might be fine for you.

#### Important Notes

- I compile this using Visual C++ Express 2010's toolset.
- Some of the editor GUI is modified to be more usable on low-res screens.
- The current OpenGL 1.x compatible renderer is labled as the GLES1 renderer as that was the name inherited from Godot 1.0.
  This name is potentially misleading since I am targeting the regular OpenGL spec.
- Some of the functions used in the renderer suggest a minimum OpenGL version of 1.5.
  Buffer objects (1.5) and multitexturing features (1.3) are used.
  I might add a way for the engine to detect if these features are available so it can run on lower versions.
- NO_THREADING is defined as there is no InterlockedCompareExchange64 function on NT 5.1 (Windows XP 32-bit).
  I don't know the full concequences of this but things seem to work fine, so, /shrug.
  This also means light baking may be broken.

#### GLES1 Known limitations

- Viewports do not render correctly in the editor, and escape the main viewport.
  The engine expects the editor viewport to use a framebuffer object, but FBOs are not implemented for the GLES1 renderer at the moment.
- Render targets/viewport textures especially do not work.
- Texture/cubemap environment background does not work.
- Not all FixedMaterial features work. FixedMaterials can only render using one texture at a time
  as their material properties are fed to the OpenGL fixed function lighting material system.
  This causes differences in rendering. Since the fixed-function pipeline lighting is vertex-based,
  material features like Emission will add color to the mesh vertices rather than the result of a texture to the surface.
  The GLES2 renderer allows you to select textures for features like specular/bump/emission, but in the GLES1 renderer
  these are treated as vertex lighting modifiers.
- ShaderMaterials and Shaders do not work AT ALL. This would require OpenGL extensions to support.

## Original README

[![GODOT](/logo.png)](https://godotengine.org)

## Godot Engine

Homepage: https://godotengine.org

#### 2D and 3D cross-platform game engine

Godot Engine is a feature-packed, cross-platform game engine to create 2D and
3D games from a unified interface. It provides a comprehensive set of common
tools, so that users can focus on making games without having to reinvent the
wheel. Games can be exported in one click to a number of platforms, including
the major desktop platforms (Linux, Mac OSX, Windows) as well as mobile
(Android, iOS) and web-based (HTML5) platforms.

#### Free, open source and community-driven

Godot is completely free and open source under the very permissive MIT license.
No strings attached, no royalties, nothing. The users' games are theirs, down
to the last line of engine code. Godot's development is fully independent and
community-driven, empowering users to help shape their engine to match their
expectations. It is supported by the Software Freedom Conservancy
not-for-profit.

Before being open sourced in February 2014, Godot had been developed by Juan
Linietsky and Ariel Manzur (both still maintaining the project) for several
years as an in-house engine, used to publish several work-for-hire titles.

### Getting the engine

#### Binary downloads

Official binaries for the Godot editor and the export templates can be found
[on the homepage](https://godotengine.org/download).

#### Compiling from source

[See the official docs](http://docs.godotengine.org/en/latest/development/compiling/)
for compilation instructions for every supported platform.

### Community

Godot is not only an engine but an ever-growing community of users and engine
developers. The main community channels are listed [on the homepage](https://godotengine.org/community).

To get in touch with the developers, the best way is to join the
[#godotengine IRC channel](https://webchat.freenode.net/?channels=godotengine)
on Freenode.

### Documentation and demos

The official documentation is hosted on [ReadTheDocs](http://docs.godotengine.org).
It is maintained by the Godot community in its own [GitHub repository](https://github.com/godotengine/godot-docs).

The [class reference](http://docs.godotengine.org/en/latest/classes/)
is also accessible from within the engine.

The official demos are maintained in their own [GitHub repository](https://github.com/godotengine/godot-demo-projects)
as well.

There are also a number of other learning resources provided by the community,
such as text and video tutorials, demos, etc. Consult the [community channels](https://godotengine.org/community)
for more info.

[![Build Status](https://travis-ci.org/godotengine/godot.svg?branch=master)](https://travis-ci.org/godotengine/godot)
[![Code Triagers Badge](https://www.codetriage.com/godotengine/godot/badges/users.svg)](https://www.codetriage.com/godotengine/godot)
