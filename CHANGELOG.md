# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.2.0] - 2025-04-15

### Added
- Added the 'Info Bar', a bar at the bottom of the 'Grid Editor' that displays information about the pixel the mouse is hovering over, such as its coordinates and actual color (in case a channel is deactivated).
- Added for the 'Inspector' a way to close it in a conventional way, the X button.
- The layer now keeps track of any changes you make. When you close the window, a panel will appear asking whether you want to save or discard the changes.
- If you try to open a layer while another (or the same) layer window is already open, a panel will appear asking whether to cancel opening the new layer or discard the changes to proceed.

## [1.1.1] - 2024-08-12

### Patch
- Fixed paint tool not updating paint color when edited, copied or affected.
- Fixed the generation of coordinates of cell for non-square grid.
- Fixed the update of grid when cleared.

## [1.1.0] - 2024-07-27

### Breaking Changes
- Updated PixelMaps/PixelLayer serialized data to improve performance, break the asset so i introduced a conversions for each legacy asset. (support limited to 1.1.x versions only)
  
  Each asset will display a warning if it is a legacy version and provide a "Rebuild" button to convert to the newer version.
  
  WARNING: Converting will result in the loss of references to these assets. Manual re-assignment is required.

### Changes
- Implemented optimizations and cleanup from the previous prototype version.
- Optimized grid rendering: replaced individual VisualElement cells with a single Paint2D operation for the entire grid. (rendered in segments to avoid vertex limits)
- The new grid implementation significantly reduces code complexity, improving performance without requiring StyleColor caching for VisualElement.
- Simplified code for generating fields for Color2Object.

## [1.0.3] - 2024-06-14

### Fixed
- Fixed an error that occurred when deleting a sublayer during the loop that displays sublayer buttons. The sublayer is now cached and deleted outside the loop.

## [1.0.2] - 2024-06-10

### Fixed
- To keep track asset reference, now PixelLayer and Session have a dedicated member and method.
- PixelPack cache the data instead of PixelOutput to avoid to use the cached real color of the first PixelOutput during fetch iteration.

### Removed
- Removed Int16 (aka short) because don't have a dedicated field. (and because manage number field as string and can clamp the value without do manually)

## [1.0.0] - 2024-06-01

1.0.0 Changelog is generated from git commits.

### Added
- Implemented tab support for managing multiple tools within a single window.
- Added basic grid pixel functionality and drawing capabilities.
- Introduced new responsive data support for improved user interaction.
- Upgraded variables to prepare for upcoming features, such as the inspector.
- Initiated prototyping of the inspector and completed its features.
- Project marked ready for the runtime phase, a significant milestone.

### Changed
- Converted the project from a Unity-based implementation to a standalone plugin project.
- Updated serialization and deserialization methods to support various data types.
- Improved RGB channel value loading for better synchronization.
- Streamlined creation process of pixel editor toolbar and made minor adjustments.
- Simplified tab creation and binding processes to enhance navigation.
- Styled Color2Object and polished toggle and setting UI for better user interaction.
- Centralized text and values for better consistency.

### Fixed
- Corrected associations update mechanism to ensure accuracy.
- Fixed various bugs related to grid management and color association updates.
- Resolved typos and micro-optimized ColorOrder cache for better performance.
