# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.3] - 2024-06-14

## Fixed
- Fixed an error that occurred when deleting a sublayer during the loop that displays sublayer buttons. The sublayer is now cached and deleted outside the loop.

## [1.0.2] - 2024-06-10

### Fixed
- To keep track asset reference, now PixelLayer and Session have a dedicated member and method
- PixelPack cache the data instead of PixelOutput to avoid to use the cached real color of the first PixelOutput during fetch iteration

### Removed
- Removed Int16 (aka short) because don't have a dedicated field (and because manage number field as string and can clamp the value without do manually)

## [1.0.0] - 2024-06-01

1.0.0 Changelog is generated from git commits

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
