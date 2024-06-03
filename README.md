# **✨ Pixel Mapper Documentation ✨**

This guide covers the Pixel Mapper, a tool for mapping pixel values to data types. The Pixel Mapper allows for the creation of complex setups using a grid layout.

## **🗂️ Index**

1. [🚀 Getting Started](#getting-started)
2. [📦 Managing Assets](#managing-assets)
3. [🛠️ Description of the Tool](#description-of-the-tool)
    - [🖌️ Grid Editor](#grid-editor)
        - [🔧 Toolbar](#toolbar)
        - [📊 Grid](#grid)
        - [🔍 Inspector](#inspector)
    - [🎨 Color2Object](#color2object)
        - [🎨 Relation Color-Integer](#relation-color-integer)
        - [📜 Relation Color-Scriptable](#relation-color-scriptable)
    - [⚙️ Settings](#settings)
        - [🌈 RGB Channels](#rgb-channels)
4. [📖 How to Use Grid Editor](#how-to-use-grid-editor)
    - [🎨 Color Selection](#color-selection)
    - [🔧 Tools](#tools)
        - [🖌️ Paint Tool](#paint-tool)
        - [🔍 Inspect](#inspect)
        - [🎯 Picking](#picking)

## **🚀 Getting Started**

To begin using the Pixel Mapper, follow these steps:

1. Copy this Git repository URL: [PixelMapper](https://gitlab.com/davide.balan.official/pixelmapper.git).
2. In the Unity window, go to "Assets" -> "Import Package" -> "Custom Package" and paste the Git repository URL to import the plugin.
3. Create a new Pixel Mapper object by selecting 'Create > MatrixMapData' in the 'Assets' panel or by right-clicking in the inspector. This will launch a wizard to name the main asset, the first sub-asset, and set the grid size for all sub-assets.

## **📦 Managing Assets**

From here, you can manage your assets effectively:

- **➕ Create a New Layer**: Name the new layer "Untitled".

![CreateNewSubLayer](CreateNewSubLayer.gif)

- **✏️ Rename a Layer**: Select the sub-asset, change its name in the inspector by editing the 'Name' field, and click 'Rename'.

![RenameSubLayer](RenameSubLayer.gif)

- **🔘 Buttons Overview**: You'll see a list of buttons with the names of the sub-assets. Click on one to open the tool, or click '❌' to remove the sub-asset (at least one sub-asset must remain). There’s also a button for quick access to the last layer you opened.

![SubLayersExample](SubLayersExample.png)

## **🛠️ Description of the Tool**

The tool is divided into three main sections:

- **🖌️ Grid Editor**: View and edit the grid.
- **🎨 Color2Object**: Associate pixels with values of a selected type across the grid.
- **⚙️ Settings**: Configure the type associated with the pixel and specify which RGB channels to use.

### **🖌️ Grid Editor**

#### **🔧 Toolbar**

- **🎨 Color Selector**: Choose the pen color and see a preview of the selected color.
- **🗑️ Clear Grid**: Reset the grid to the default color (White).
- **🔧 Tools**:
  - **🖌️ Paint Tool**: Draw with the selected color (LMB) or erase (RMB).
  - **🔍 Inspect**: Select a pixel to see its details.
  - **🎯 Picking**: Copy the selected pixel’s color to the color selector.

![Toolbar](GridEditorToolbar.png)

#### **📊 Grid**

The grid is the main workspace where you view and draw pixels. When using the **Inspect** tool, the selected pixel is highlighted with a contrasting border.

![Grid](GridEditor.png)

#### **🔍 Inspector**

The inspector panel shows the true color of the pixel regardless of any RGB channel filters applied, an editable hexadecimal color value, and the pixel's coordinates.

![Inspector](InspectAPixel.gif)

### **🎨 Color2Object**

#### **:1234: Relation Color-Integer**

![Color2Object](Color2ObjectWithInteger.png)

#### **📜 Relation Color-ScriptableObject**

![Color2ObjectScriptable](Color2ObjectWithGenericScriptableObject.png)

In this panel, you can associate pixels with values of a selected type for the entire grid. All colors in the grid are included.

### **⚙️ Settings**

There are some settings that can change the behaviour and representation of the tool.

![Settings](Settings.png)

## **📖 How to Use Grid Editor**

### **🎨 Color Selection**

The color can be set by editing the RGB channels in **Draw Color** and looking at **Color Preview** to know what color will be used.

![DrawColorAndPreview](DrawColorAndPreview.png)

### **🔧 Tools**

A collection of tools used on the grid:

![GridEditorTools](GridEditorTools.png)

#### **🖌️ Paint Tool**

With this tool, you can paint on the grid. To paint, click/drag with the Left Mouse Button and erase with the Right Mouse Button.

#### **🔍 Inspect**

With this tool, you can click on a pixel in the grid to view details about the selected pixel, including the true color, RGB fields, hexadecimal value, and coordinates.

![GridEditorInspector](GridEditorInspector.png)

#### **🎯 Picking**

With this tool, you can pick the color of the selected pixel and transpose it to **Draw Color**.

![PickingAPixel](PickingAPixel.gif)

## TODO of README

- Explain how to use *Color2Object* and create a file with supported type
- Explain what the settings affect the tool
- Explain coordinate of the grid work
- Explain how a grid of color work combined with *Color2Object*
- Explain i can turn off a RGB channel and for what purpose
- Explain how use the assets
  - First using sub asset
  - Later using main asset
- Create a demo project with some examples
