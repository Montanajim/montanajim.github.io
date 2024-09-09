# Unreal 5 crashing



## Here is a possible fix.

Change the following in project settings:

- Engine - Rendering -> Shadows
  - Change the Shadow Map Method to Shadow Maps. (Virtual Shadow Mapping causing problems)
- Platforms - Windows
  - Change the Shaders from SM6 to SM5



10/19/23