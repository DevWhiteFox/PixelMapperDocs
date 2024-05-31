# **Pixel Mapper Documentation**

This guide covers the Pixel Mapper, a tool for mapping pixel values to a data types. The Pixel Mapper allows for the creation of complex setups using a grid layout.

## **Getting Started**

To begin using the Pixel Mapper, you need to create a new Pixel Mapper object. In the 'Assets' panel or by right-clicking in the inspector, select 'Create > MatrixMapData'.

This will launch a wizard where you'll name the main asset and the first sub-asset. You'll also set the grid size for all sub-assets.

## **Managing Assets**

![CreateNewSubLayer](CreateNewSubLayer.gif)

From here, you can create a new layer named "Untitled".

![RenameSubLayer](RenameSubLayer.gif)

To rename a layer, select the sub-asset, change its name in the inspector by editing the 'Name' field, and click 'Rename'. The sub-asset will be selected immediately after its creation.

### **Buttons Overview**

You'll see a list of buttons with the names of the sub-assets. Click on one to open the tool, or click 'X' to remove the sub-asset (at least one sub-asset must remain).

There’s also a button for quick access to the last layer you opened.

## **Using the Tool**

![Tabs](TabsOfTheTool.png)

The tool is divided into three sections:
- **Grid Editor**: View and edit the grid.
- **Color2Object**: Associate pixels with values of a selected type across the grid.
- **Settings**: Configure the type associated with the pixel and specify which RGB channels to use.

### **Grid Editor**

#### **Toolbar**

![Toolbar](GridEditorToolbar.png)

- **Color Selector**: Choose the pen color and see a preview of the selected color.
- **Clear Grid**: Reset the grid to the default color (White).
- **Tools**:
  - **Paint Tool**: Draw with the selected color (LMB) or erase (RMB).
  - **Inspect**: Select a pixel to see its details.
  - **Picking**: Copy the selected pixel’s color to the color selector.

#### **Grid**

![Grid](GridEditor.png)

The grid is the main workspace where you view and draw pixels. When using the **Inspect** tool, the selected pixel is highlighted with a contrasting border.

#### **Inspector**

![Inspector](InspectAPixel.gif)

The inspector panel shows the true color of the pixel regardless of any RGB channel filters applied, an editable hexadecimal color value, and the pixel's coordinates.

### **Color2Object**

#### **Relation Color-Interger**

![Color2Object](Color2ObjectWithInteger.png)

#### **Relation Color-Scriptable**

![Color2ObjectScriptable](Color2ObjectWithGenericScriptableObject.png)

In this panel, you can associate pixels with values of a selected type for the entire grid. All colors in the grid are included.

### **Settings**

![Settings](Settings.png)

In the settings panel, you define the type associated with the pixel.

#### **RGB Channels**

There are three toggles to include or exclude RGB channels in pixel representation. For example, turning off the Red channel will display RGB(1f, 1f, 0.5f) as RGB(0f, 1f, 0.5f). This affects representation and association only; the actual pixel color remains unchanged for data purposes.
