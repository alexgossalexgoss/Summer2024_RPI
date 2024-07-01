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
- A note about "Opacity" in Substance Painter, to get the most apparent effects, use very contrasting masks or brushes. If you are working procedurally (say, wanting to make glass dirty around the edges) you can add a "Levels" effect above your procedural mask and drag the sliders to crush the highlights and shadows

### Maya Scale Tips
- 3D models have no inherent reference to scale. Software interprets 3D models based on user settings.
- Maya and Unreal both use centimeters for their interpretation of scale.
- However, Maya's viewport is misleading.
- The default grid is quite small relative to the kinds of world Unreal expects users to build in. 
- To prove this, we can import from the shared "ReferenceModels" folder, "SM_UE_Manny.fbx".
- This is the default mannequin from UE.
- Let's increase the length and width of our grid in Grid options somewhere between ***100 and 500*** units.
  ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/1258f85b-e991-48d6-b5db-03fd835d29b0)
- Notice our model does not change size.
- If you were building before based on the default grid as reference to scale, you'll need to manually scale your model up.
  If scaling multiple components, this can break the configuration of an assembly. 
- Try deleting history for all components, and check that they all share the same origin before scaling.
- scale object based on real world units and in reference to "Manny"
- orient (translate/rotate) object so base rests on ground/grid
- ask yourself how your object would need to rest with physics in mind

# Unreal

Only make changes in YOUR folder in the Student folder
- You have a private "Level" asset you can edit directly or as a child to the main level.
  
Keep your folders organized using: 
- ***Static_Meshes***
- ***Textures***
- ***Materials***
- ***Blueprints***
  
### Static Mesh Import
- in your Static_Mesh folder, import your FBX exported from Maya
- for any of these option you may have to expand various secrtions with "▶" -> "▼"
- do not use nanite
  ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/b6fa510f-8367-4732-a732-4f9c4a92e608)
- "combine meshes"
- ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/5d7cbe79-7100-4dac-b6c2-fb77a887ec4a)
- do not create materials or import texture
  ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/210282f9-8b70-480a-a19e-99ca487db517)

  
### Textures
- for Occlusion-Roughness-Metallic (ORM) textures change their compression settings to "Masks (no sRGB)" this can be batch done using Asset Actions-> " Edit Selection in Property Matrix".
![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/a39576bb-5bb9-4dee-ae36-faeb434dd8b9)
and within Property Matrix:
![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/a8a34d62-5186-4f07-a768-a85e8909c3fb)
- Quick tip: if you used the Unreal 4 texture output template from Substance Painter, you can search in your textures folder for "OcclusionRoughness"
- keep the Diffuse Maps as default
- keep Normal Maps as default
  
### Using Material Templates (Instances)
- ***Copy*** the Material Parent Instance "MI_HybridObject_Parent" from the "Copy From Here" folder into your "Materials" folder.
- From here, you can rename, edit, duplicate, and apply these as they now belong to you.
- Material Instances come with parameters and variables that you can change to customize the look of your shaders.
- To start, begin by adding your texture maps to the "0 - Texture Maps" section.
  ![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/96e139f3-6a11-45ab-96e2-9237099acd73)
- We will cover the rest of the details briefly, but feel free to explore and adjust.
- You can always hit the back arrow icon to the right of any property to reset it to its default.
One of my favorite buttons--a great tool for safe exploration!
![image](https://github.com/alexgossalexgoss/Summer2024_RPI/assets/122226156/b6eb6e59-eb4d-4a40-b224-53e9741b8ed9)

- Apply these materials by opening your static mesh object and apply them to their respective materials slots. this will ensure your materials will follow your static mesh wherever it is implemented
  
### Using the Blueprint Actor Template
- Like with the parent material, you will ***copy*** "BP_HybridObject_Parent" from the "Copy From Here" folder into your "Blueprints" folder.
- For this object, Please rename it "BP_yourLastName_yourFirstName".
- You do not need to make any edits to this blueprint.
- To use it, drag it into the viewport and edit its properties to the bottom right.
- with this object now an actor in the game level will need to add you:
	- **static mesh**
	- **name**
	- if you want to use a pedestal and how large it needs to be
	- try to position your object at eye level
- Lastly, there is a spotlight blueprint available for your use "BP_Spotlight_Child" you can use in your personal level to light your object.
	- note that its Z height should be set to 0, but the object will be positioned above the move tool. I've tailored it to be connected to the ceiling.


# Demo Notes

Improper Scale
Different Component Origins
Rotation
Emphasize real world positioning in design and orientation

Importing
Combine meshes, turn off nanite, rotation Z up

Detail Normal and Color

Copying Parameter Sections between MI's

Adding Actors

Levels (make level panel available and dock)