# **✨ Pixel Mapper Documentation ✨**

This guide covers the Pixel Mapper, a tool for mapping pixel values to data types. The Pixel Mapper allows for the creation of complex setups using a grid layout.

## **🚀 Getting Started**

To begin using the Pixel Mapper, follow these steps:

1. Copy this Git repository URL: [PixelMapper](https://gitlab.com/davide.balan.official/pixelmapper.git).
2. In the Unity window, go to "Assets" -> "Import Package" -> "Custom Package" and paste the Git repository URL to import the plugin.
3. Create a new Pixel Mapper object by selecting 'Create > MatrixMapData' in the 'Assets' panel or by right-clicking in the inspector. This will launch a wizard to name the main asset, the first sub-asset, and set the grid size for all sub-assets.

For a more detailed explanation on managing assets, refer to [Managing Assets](#managing-assets).

## **📦 Managing Assets**

From here, you can manage your assets effectively:

- **➕ Create a New Layer**: Name the new layer "Untitled".

![CreateNewSubLayer](CreateNewSubLayer.gif)

- **✏️ Rename a Layer**: Select the sub-asset, change its name in the inspector by editing the 'Name' field, and click 'Rename'.

![RenameSubLayer](RenameSubLayer.gif)

- **🔘 Buttons Overview**: You'll see a list of buttons with the names of the sub-assets. Click on one to open the tool, or click '❌' to remove the sub-asset (at least one sub-asset must remain). There’s also a button for quick access to the last layer you opened.

![SubLayersExample](SubLayersExample.png)

For a simpler overview, refer to [Getting Started](#getting-started).

## **🛠️ Description of the Tool**

The tool is divided into three main sections:

- **🖌️ Grid Editor**: View and edit the grid.
- **🔀 Color2Object**: Associate pixels with values of a selected type across the grid.
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

For a more detailed explanation on how to use these tools, refer to [How to Use Grid Editor](#how-to-use-grid-editor).

#### **📊 Grid**

The grid is the main workspace where you view and draw pixels. When using the **Inspect** tool, the selected pixel is highlighted with a contrasting border.

![Grid](GridEditor.png)

For more details on working with the grid, refer to [How to Use Grid Editor](#how-to-use-grid-editor).

#### **🔍 Inspector**

The inspector panel shows the true color of the pixel regardless of any RGB channel filters applied, an editable hexadecimal color value, and the pixel's coordinates.

![Inspector](InspectAPixel.gif)

### **🔀 Color2Object**

#### **🔢 Relation Color-Integer**

![Color2Object](Color2ObjectWithInteger.png)

#### **📜 Relation Color-ScriptableObject**

![Color2ObjectScriptable](Color2ObjectWithGenericScriptableObject.png)

In this panel, you can associate pixels with values of a selected type for the entire grid. All colors in the grid are included.

For a simpler overview of the Color2Object panel, refer to [How to Use Color2Object](#how-to-use-color2object).

### **⚙️ Settings**

There are some settings that can change the behaviour and representation of the tool.

![Settings](Settings.png)

For more detailed explanations of the settings, refer to [How to Use the Settings](#how-to-use-the-settings).

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

For a simpler overview of these tools, refer to [Grid Editor](#grid-editor).

## **📦 How to Use Color2Object**

Depending on the type selected for the Color-Object association, how you can modify it may differ, but fortunately, it works like a normal Unity inspector input field.

The supported types are indicated in [Supported Type](SupportedType.md).

For a more detailed explanation on the Color2Object panel, refer to [Color2Object](#color2object).

## **⚙️ How to Use the Settings**

### **🔣 Color Matrix Type**

This setting affects Color2Object by determining the type associated with each color. Changing this setting will clear all previous associations, so change it only once to avoid losing the associations.

### **🌈 Active (Red/Green/Blue) Channel**

This setting affects:

- The representation of the color in the **Grid Editor**, excluding some channels.
- Disabling and resetting the channel of **Draw Color** affects **Color Preview**.
- The channel deactivated in the settings will enable that channel in the inspector that allows it to be edited.
- **Color2Object** will refresh the association with the new color, and the old association will be hidden until the channel is restored to its previous state.

> Note: The amount of channel that you can turn of is two, the third channel will not turn off, because the user have to to use al least a channel to edit the grid.

For a simpler overview of the settings, refer to [Settings](#settings).

## **🔍 Explanation of How It Works Behind the Scenes**

### **🗺️ How the Grid Coordinates are Represented**

The main reason is to work natively with Unity's coordinate system.

Like Unity, the Up direction is represented by the Y-axis from bottom to top, and the Right direction is represented by the X-axis from left to right.

The coordinate system is like Unity's P(X, Y) for the direction D(Right, Up).

### **🔄 How the Data Association Works**

To get all different color for association, the tool iterate all the grid and collect unique color, for each color generate an input field for the type selected.
Each field when edited will update the association list ready to be saved.

> Example: IntegerField -> int -> Dictionary<Color, *object*> (int become *object* and insered as new value) 

### **🔄 How Data of Association is saved and loaded**

#### **🔧 From Tool to Sublayer**

After finishing assigning a value to the association, the data is assigned as a C# *object*.

Once we click on **Save**, we parse the *object* byte by byte, resulting in an array of bytes that can be serialized.

For the conversion object->byte[], the type must have System.Serializable. For types that can't be natively serialized, I use a custom method to organize data for serialization.

> For example, a Vector3 will become float[3], which is natively serialized. In summary, Vector3 -> float[3] (surrogate) -> *object* -> byte[].

#### **🔄 From Sublayer to Tool or for User Use**

This works like the "From Tool to Sublayer" process but in reverse.

For example, in the tool with a Vector3, byte[] is used to build an *object*. Based on the type in **Settings**, **Color2Object** creates the appropriate field, casts it to the correct type (or surrogate), and sets the field with the value.

Meanwhile, a user who wants the data of a specific pixel (using coordinates) will follow the same process: byte[] -> build *object* -> cast to surrogate (if needed) -> rebuild original type, and lastly, provide it to the player.

> Note: Retrieving the data requires specifying the type as Generic, which can differ from the type of the sublayer only if it can be cast; otherwise, it will give an error.

> Example: T must be a type that can cast the data of the type set in the settings.

    PixelPack<T> pixelPack = new PixelPack<T>(pixelLayers);
    PixelOutput<T> point = pixelPack.GetPixelOutput(1,4);

### **🌈When i need to deactivate a RGB channel**

The amount of association with:

- Three channels active is: 16777216 colors
- Two channels active is: 65536 color
- One channel active is: 256 color

It is rare to use 16,777,216 or 65,536 colors, so this allows us to use the unused channel value of each pixel as we please.

> For example we deactivate the blue channel, and get some *PixelOutput<T>*, that contain the real color;
>
> We get two pixel A = RGB(0.5f, 0.4f, 1f) and B = RGB(0.5f, 0.4f, 0.5f)
>
> During association the two pixel look like this A = RGB(0.5f, 0.4f, 0f) and B = RGB(0.5f, 0.4f, 0f), so this will return the same value
>
> So for the association they are the same, but in reality the have blue channel with different value, imagine having the type on Vector3, the *PixelOutput<T>*s will contain:
>
> - Data A -> Vector3(3.0f, 2.0f, 3.0f) and RGB(0.5f, 0.4f, 1f)
>
> - Data B -> Vector3(3.0f, 2.0f, 3.0f) and RGB(0.5f, 0.4f, 0.5f)
>
> In this scenario the Red and Green can the ignored and focus on blue channel, and use the value of blue channel as scale, offset and ect... depend of the necessity of the user 

### **📦How use a sublayer asset**

Example:

Script that instantiate a prefab at xy position of grid but only if data is not 0, z in 1 or 0 depend of the blue channel value
```csharp
PixelPack<int> pack = new(sublayerAsset);

PixelOutput<int> output = pack.GetPixelOutput(1, 5);
        
pack.IterateMatrix((x, y, color, data) =>
{
    if(data == 0) return;
            
    if(color.b > 0.5f) Instantiate(prefab, new Vector3(x, y, 0), Quaternion.identity);
    else Instantiate(prefab, new Vector3(x, y, 1), Quaternion.identity);
 });
```

### **📦How use the main asset**

Same as using sublayer directlly, but is possible to get sublayer  by index
```csharp
PixelPack<int> pack = new(mainAsset[0]);
        
//Omitted for brevity
```
Or by using the name of sublayer
```csharp
PixelPack<int> pack = new(mainAsset["sublayerName"]);
        
//Omitted for brevity
```

### **What are the purpose of PixelPack and PixelOutput**

PixelPack is used to fetch, cache and then serve to the user the pixel data by requesting a specific coordinate or iterating completely.

PixelOutput help PixelPack to have an instance of the result of association that hold the real color and the data associated and cache it if requested frenquenlty and the used can obtain it by *pack.GetPixelOutput(x, y)* that allow to get color and data.

```csharp
PixelOutput<int> output = pack.GetPixelOutput(1, 5);
Color color = output.pixelColor;
int data = output.data;
```

### *❗Common errors*

To avoid confusion caused by errors that you believe stem from the tool but actually result from its usage, follow these guidelines.

#### *💁User Code*

##### *🚧PixelPack type don't match type of sublayer*

If you have a **PixelPack<Vector3>** but the sublayer is set with **float**, the tool will indicate that the types are not compatible. However, it will not stop the rest of the code from executing.

##### **❗User error in _IterateMatrix_**

Sometimes, you might encounter an error indicating that the callback _**action**_ failed due to an error in the lambda function within the IterateMatrix function.

## *🎨Samples*

I created a project with several mini-projects that demonstrate different ways to use the tool as I conceived it. This means you can use it in more creative ways.

[🔗Link to the project samples](https://github.com/DevWhiteFox/PixelMapperExamples/tree/main)

## Unity version supported

- 2022.3
- 6000.0 (Previe w)
