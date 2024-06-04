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
    - [:twisted_rightwards_arrows: Color2Object](#color2object)
        - [:1234: Relation Color-Integer](#relation-color-integer)
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

### **:twisted_rightwards_arrows: Color2Object**

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

## How to Use Color2Object

Depending on the type selected for the Color-Object association may differ how you can modify it, but fortunately it works like a normal Unity inspector input field.

The type supported is indicated in [Supported Type](SupportedType.md)

## How to Use the Settings

### Color Matrix Type (to rename in Association Color-Type)

This setting affect Color2Object what type is associate for each color, this will clear all previous association so change once this settings to avoid lose the associations.

### Active (Red/Green/Blue) Channel

This setting affect:

- The rapresentation of the color of the **Grid Editor** that exclude some channel.
- Will disable and reset the channel of **Draw Color** that affect **Color Preview**.
- In the inspector will be enabled the channel deactivated to allow the editing.
- **Color2Object** will refresh the association with the new color and the old association will hidden until restore the channel old state.

## Some explanation how work behind the scene

### How the coordinate of the grid rappresent

The main reason is to to work nativelly the coordinate system of Unity.

Like unity the Up is rappresented with the Y from bottom to up, and the Right is rappresented with X from left to right.

The coordinate is like unity P(X, Y) for the direction D(Right, Up)

### How the data of association work

#### From tool to sublayer

After finish assign a value to the association, the data is assigned as C#'s *object*;

Once we blick on **Save** we parse the *object* byte per byte that result as array of byte that allow to be serialize.

The conversion object->byte[] the type require have System.Serialize, and for type that can't be nativelly serialize i use a custom way to organize data in order to serialize;

Example is Vector3 will become float[3] that is nativelly serialized, resumed is Vector3 -> float[3] (surrogate) -> *object* -> byte[]

#### From sublayer to Tool or to be used from user

This work like **From tool to sublayer** but in reverse.

Example with of happen in tool with a Vector3, byte[] is used to build an *object* and in **Color2Object** base on type in **Settings** create the right field and cast to the right type (or surrogate) and set the field with the value

Meanwhile the used that want the data of specific pixel (by using coordinate) will do the same thing byte[] -> build *object* -> casted to surrogate (is it's needed) -> rebuild orginal type and lastly given to player.

Note: Retreive the data have to specify the type as Generic that can differt from type of sublayer only if can be casted, otherwise will give and error.

Example: T must be a type that can cast the data of the type set in the settings

    PixelPack<T> pixelPack = new PixelPack<T>(pixelLayers);
    PixelOutput<T> point = pixelPack.GetPixelOutput(1,4);

## TODO of README
- Explain how a grid of color work combined with *Color2Object*
- Explain i can turn off a RGB channel and for what purpose
- Explain how use the assets
  - First using sub asset
  - Later using main asset
- Create a demo project with some examples
