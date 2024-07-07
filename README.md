# Table of Contents
1. [Object Preparation](#object-preparation)
   - [Substance Painter](#substance-painter)
   - [Maya Scale Tips](#maya-scale-tips)
2. [Perforce](#Accessing-and-Submitting-Project-Files-from-Perforce)
 - [Where Is the project in Perforce?](#where-is-the-project-in-perforce)
 - [What am I responsible for submitting to Perforce?](#what-am-i-responsible-for-submitting-to-perforce)
 - [What should I NOT submit to Perforce?](#what-should-i-not-submit-to-perforce)
3. [Importing and Adding your Object in Unreal Engine 5.4](#importing-and-adding-your-object-in-unreal-engine-54)
   - [Static Mesh Import](#static-mesh-import)
   - [Textures](#textures)
   - [Using Material Templates (Instances)](#using-material-templates-instances)
   - [Editing your level](#editing-your-level)
   - [Using the Blueprint Actor Template](#using-the-blueprint-actor-template)

# Object Preparation
***Before beginning your Substance Painter work***, I recommend labelling your object's materials clearly and meaningfully in Maya's Hypershade, these will translate to Substance Painter *and* Unreal engine and will carry through into your texture sets. A little but of organization now will make the work you do in Unreal breezy.

## Substance Painter
- If you want to use opacity, change your Shader Settings (top right ball icon) to "pbr-metal-rough-with-alpha-blending"
- ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/a16ecf09-a63a-49e3-945b-5f0b616f4e7d)
- Use the "Unreal Engine 4" Preset for exporting
- You will end up with 3-4 texture maps per texture set/material slot
- "Emissive" textures will export only for those texture sets that you have manually designated in "Texture Set Settings"
- ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/125384d3-5c86-4709-a7db-d5604fc3f07e)
- Likewise, "Opacity" (packed in the A channel of your Diffuse RGBA texture map) will not contain meaningful data unless using opacity in your texture set.
- A note about "Emissive" in Substance Painter, you won't witness much difference in your emissive painting unless you change your "Shader Settings" and boost the "Emissive Intensity" slider!
- to further visualize emissive effects, visit "Display Settings" (top right monitor icon), scroll down and check "Activate Post Effects" and check "Glare"
- ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/3cd25a90-9f87-4c9d-9aff-899111454af0)
- A note about "Opacity" in Substance Painter, to get the most apparent effects, use very contrasting masks or brushes. If you are working procedurally (say, wanting to make glass dirty around the edges) you can add a "Levels" effect above your procedural mask and drag the sliders to crush the highlights and shadows.
- Try to keep your textures under 2048x2048.

### Maya Scale Tips
- 3D models have no inherent reference to scale. Software interprets 3D models based on user settings.
- Maya and Unreal both use centimeters for their interpretation of scale.
- However, Maya's viewport is misleading.
- The default grid is quite small relative to the kinds of world Unreal expects users to build in. 
- To prove this, we can import from the shared "ReferenceModels" folder, "SM_UE_Manny.fbx".
- This is the default mannequin from UE.
- Let's increase the length and width of our grid in Grid options somewhere between ***100 and 500*** units.
- ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/1258f85b-e991-48d6-b5db-03fd835d29b0)
- Notice our model does not change size.
- If you were building before based on the default grid as reference to scale, you'll need to manually scale your model up.
  If scaling multiple components, this can break the configuration of an assembly. 
- Try deleting history for all components, and check that they all share the same origin before scaling.
- scale object based on real world units and in reference to "Manny"
- Manny lives here on the Perforce Depot:
- ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/700fc223-d20a-49c1-91b0-3165b424170f)
- orient (translate/rotate) object so base rests on ground/grid
- ask yourself how your object would need to rest with physics in mind

# Accessing and Submitting Project Files from Perforce

Only make changes in YOUR folder in the Student folder
- You have a private "Level" asset you can edit directly or as a child to the main level.

## Where Is the project in Perforce?
![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/8b5add95-bcb7-4748-87d4-c79251ed6f0d)
## What am I responsible for submitting to Perforce?
Only submit your folder from the hierarchy of:

<pre>
shared
├── Unreal
│   ├── Hybrid_Objects_UE_5-4
│   │   ├── Content
│   │   │   ├── Student_Folders
│   │   │   │   ├── <b>Your_Folder</b>
</pre>


- ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/e9c32fb6-0103-46ae-984d-835974bf6c4a)
## What should I NOT submit to Perforce?
any other folder or asset not in your own folder.

# Importing and Adding your Object in Unreal Engine 5.4

### Keep your folders organized using: 
- ***Static_Meshes***
- ***Textures***
- ***Materials***
- ***Blueprints***
  
## Static Mesh Import
- in your Static_Mesh folder, import your FBX exported from Maya
- for any of these option you may have to expand various secrtions with "▶" -> "▼"
- do not use nanite
- ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/b6fa510f-8367-4732-a732-4f9c4a92e608)
- "combine meshes"
- ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/5d7cbe79-7100-4dac-b6c2-fb77a887ec4a)
- do not create materials or import texture
- ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/210282f9-8b70-480a-a19e-99ca487db517)
- If your model comes in at a funny angle or a weird size, check your maya scene, and try importing again and resetting the import settings to default

  
## Textures
- for Occlusion-Roughness-Metallic (ORM) textures change their compression settings to "Masks (no sRGB)" this can be batch done using Asset Actions-> " Edit Selection in Property Matrix".
- ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/a39576bb-5bb9-4dee-ae36-faeb434dd8b9)
- and within Property Matrix:
- ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/a8a34d62-5186-4f07-a768-a85e8909c3fb)
- Quick tip: if you used the Unreal 4 texture output template from Substance Painter, you can search in your textures folder for "OcclusionRoughness"
- keep the Diffuse Maps as default
- keep Normal Maps as default
  
## Using Material Templates (Instances)
- ***Copy*** the Material Parent Instance "MI_HybridObject_Parent" from the "Copy From Here" folder into your "Materials" folder.
- From here, you can rename, edit, duplicate, and apply these as they now belong to you.
- Material Instances come with parameters and variables that you can change to customize the look of your shaders.
- To start, begin by adding your texture maps to the "0 - Texture Maps" section.
- ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/96e139f3-6a11-45ab-96e2-9237099acd73)
- We will cover the rest of the details briefly, but feel free to explore and adjust.
- You can always hit the back arrow icon to the right of any property to reset it to its default.
One of my favorite buttons--a great tool for safe exploration!
- ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/b6eb6e59-eb4d-4a40-b224-53e9741b8ed9)
- Apply these materials by opening your static mesh object and apply them to their respective materials slots. this will ensure your materials will follow your static mesh wherever it is implemented
- ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/8fb25f8d-88e9-4bdf-b3de-4fb2a4108acb)

## Editing ***your*** level
- first, make sure you have the levels panel available in the engine workspace.
- go to window -> levels
- ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/6ae8f9c7-e987-4f9b-be15-acdc38eb63ef)
- I like to dock this panel next to the outliner--but it's up to you.
- In the Levels Panel, you can expand the StudentLevels folder.
- Find your level, and select "Make Current"
- ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/7f7cf72c-d2ae-48cf-b103-d3297a01e3b8)
- Please only edit your own level.
- You can edit your level in isolation as well but double clicking on your level in the content browser, however, you might not see much until you've added your spotlight
  
## Using the Blueprint Actor Template
- Like with the parent material, you will ***copy*** "BP_HybridObject_Parent" from the "Copy From Here" folder into your "Blueprints" folder.
- For this object, Please rename it "BP_yourLastName_yourFirstName".
- You do not need to make any edits to this blueprint via the content browser.
- To use it, drag it into the viewport with ***your level active*** and edit its properties to the bottom right.
- ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/e9a277ef-8242-4d6f-a886-70b1de1a4dfa)
- with this object now an actor in the game level will need to add you:
	- **static mesh**
	- **name**
	- if you want to use a pedestal and how large it needs to be
	- try to position your object at eye level
- Lastly, there is a spotlight blueprint available for your use "BP_Spotlight_Child" you can use in your personal level to light your object.
	- note that its Z height should be set to 0, but the object will be positioned above the move tool. I've tailored it to be connected to the ceiling.
 - You can toggle off and on other levels. This is often necessary to better navigate and select elements. Whatever you do, please ***do not*** save or push to Perforce, the Persistent Level: L_2411
 - ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/7380ba1c-81d1-4f5c-a543-793c12b04109)

 - When you save your level, all of your edits will save.
 - ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/f216a1dc-799a-4690-8b1c-0d800d8f4c39)
 - Make sure all of your textures, static meshes, and materials are saved. Do not save the Persisent Level if you made any changes.

