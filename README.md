# ExportCodeOfMaterial

Export materials to HLSL shader code files for analysis and debugging.

## Overview

ExportCodeOfMaterial is an editor plugin that converts UE materials and Niagara systems into readable HLSL code. It extracts material properties, shader parameters, generated HLSL code, and Niagara emitter scripts into markdown files that can be reviewed, shared, or used for learning shader development.

## Installation

1. Open **Edit > Plugins** in Unreal Editor
2. Search for **Export Code Of Material**
3. Enable the plugin
4. Restart the editor

### Dependencies

- EditorScriptingUtilities (enabled by default)

## Configuration

Configure the plugin via **Project Settings**:

1. Go to **Project Settings > Export Code Of Material**
2. Set the **Export Output Directory** path
3. Set the **Export NiagaraHLSL Output Directory** path

![HLSL Code Export Settings](HLSLCode_Export_Settings.jpg)

Default output folders:
- Material: `ProjectDir/ExportedMaterialHLSL/`
- Niagara: `ProjectDir/ExportedNiagaraHLSL/`

## Usage

### Console Commands

Open the console (~) and type:

```
ExportMaterialHLSL
```
Export all materials under `/Game/` to the output folder. Default: `ProjectDir/ExportedMaterialHLSL/`

```
ExportNiagaraHLSL
```
Export all Niagara Systems under `/Game/` to the output folder. Default: `ProjectDir/ExportedNiagaraHLSL/`

### Export Selected Materials

1. Select one or more materials in the Content Browser
2. Right-click to open the context menu
3. Select **Export HLSL Code**

![Export Selected Material](Export_Selected_Material.jpg)

### Export Selected Niagara Systems

1. Select one or more Niagara Systems in the Content Browser
2. Right-click to open the context menu
3. Select **Export Niagara HLSL Code**

![Export Selected Niagara](Export_Selected_Niagara.jpg)

### Export All Materials

1. Open the Asset menu in the Content Browser
2. Select **Export Material HLSL**

![Export All Material HLSL](ExportAllMaterial_HLSL.jpg)

### Export All Niagara Systems

1. Open the Asset menu in the Content Browser
2. Select **Export Niagara HLSL**

![Export All Niagara](ExportAllNiagara_HLSL.jpg)

## Export Examples

### Material Export Output

Each material export creates a `.md` file containing:

- **Material Properties**: Blend mode, shading models, two-sided, opacity mask
- **Material Parameters**: Scalar, vector, texture, and static switch parameters
- **Material Input Section**: Custom expression functions and input connections
- **Full HLSL Code**: Generated shader code

![Example Material HLSL Export](Example_Material_Exported_HLSLCode.jpg)

### Niagara Export Output

Each Niagara export creates a `.md` file containing:

- **Niagara Properties**: System configuration, emitter details
- **Emitter Scripts**: Script types and usage
- **Generated GPU HLSL Code**: Per-emitter shader code

![Example Niagara HLSL Export](Example_Niagara_Exported_HLSLCode.jpg)

### Alternative HLSL Viewing Methods

If HLSL generation fails, try these alternatives:

**Method 1 - Material Editor**
- Open material in Material Editor
- Window > Shader Code > HLSL Code

**Method 2 - Console Command**
- Open Output Log console
- Type: `r.ShaderDevelopmentMode 1`
- Compile material
- Check: `ProjectDir/Saved/HLSLCode/`


## Target Users

### Who Can Be Benefits

- **Technical Artists** - Understand shader logic to communicate effectively with engineers
- **Shader Developers** - Analyze compiled shaders for performance optimization and debugging
- **Graphics Engineers** - Debug shader compilation issues and verify parameter usage
- **Technical Directors** - Review material standards across the project team
- **Artists Migrating from Other Engines** - Learn HLSL by studying UE material implementations

### Use Cases

| User | Use Case |
|------|---------|
| Technical Artist | "Why is my material not responding to light?" - Check shading model settings |
| Shader Developer | "Is this texture sampled only once?" - Review generated HLSL |
| Graphics Engineer | "Shader compilation failed" - Extract input section for debugging |
| Technical Director | Enforce material standards - Batch export all materials for review |

## Technical Details

- **Supported Assets**: Material, Material Instance, NiagaraSystem
- **Output Format**: Markdown (.md)
- **Platform Support**: Win64; The plugin should work for Mac, Linux but do not test. 
- **Engine Version**: UE 5.6+