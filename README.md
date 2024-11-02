## GDXP - What is this?

GDXP is a fork of Godot 2.1.7 RC that targets legacy Windows for fun, and implements an OpenGL 1.x compatible renderer.  
**GDXP is unofficial and not affiliated with the Godot project.**  
If you're looking for the regular version of Godot, you can find it here: https://godotengine.org

The target is currently just 32-bit Windows XP, but the GLES1 rasterizer should be portable to other platforms that implement OpenGL.
I only develop on Windows, so I have not explored other platforms.  
"GDXP" is kind of a temporary name but I have nothing better.

You can check what I've done so far and what I have in mind here:  
[Changelog](/xp_changes.md)  
[Ideas/Plans](/xp_ideas.md)  

#### Can I use this to load existing games?

This version of Godot is not intended as a drop-in replacement for Godot 2 games, and is an enthusiast version made for my own purposes.
I may add, change, or remove features as intended for my own use.  
The GLES1 rasterizer has fundamental differences from the GLES2 rasterizer.
Existing games made for Godot 2 target the GLES2 renderer, but this fork uses the GLES1 renderer by default for compatibility reasons.  
If you load a GD2 project in this, it might not look correct without tweaking the video driver setting.  
This engine also has fundamental backwards incompatible changes made to it since Godot 2.1.

#### Should I use this over modern Godot?

Unless your target is legacy PCs, you shouldn't. This fork isn't intended to replace modern Godot versions.
Instead, my intention is to make game development on legacy/retro platforms more bearable.
Basing this engine on an older, simpler, and more compatible version of Godot was better in every way than making my own entirely new engine from scratch.

If you're looking to make a retro style video game, you can do that just fine with any newer engine if you wrangle the shaders.
If you're the retro PC enthusiast type that's willing to put up with an old version of Godot despite its quirks, 
because you want your game to run on hardware it looks like it should, this version would be better than using Godot 1 or 2 directly.

Keep in mind that Godot 2 was built from already outdated technology, and the workflow isn't the same as a modern engine.
You may need to optimize your games well if you intend to build anything substantial.

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
- Sphere mapping looks different between GLES1 and GLES2 since GLES1 uses the texgen of OpenGL, while GLES2 uses a different technique.
  Textures used with texgen sphere mapping are also upside down.
- Meshes that use vertex colors alongside features like Lighting do not work. Need to explore GL_COLOR_MATERIAL.

#### GLES1 Known limitations

- Certain editor gizmos and vertex colored meshes render as white.
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
for more info.

#### Attributions

This software uses portions of [Godot 3](https://github.com/godotengine/godot/tree/3.x) source code.  
As it is impossible for me to individually credit every contributor's line of code that I've used, I decided to include the full contributor's list.  
I have also updated the visible copyright dates to match Godot 3's.  
I've done my best to attribute them correctly. If I've made a mistake, create an issue about it and we can work it out.
