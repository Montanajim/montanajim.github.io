# Geometry

https://www.worldofleveldesign.com/categories/ue4/bsp-01-what-is-bsp.php



To create the initial layout of the environment, don't jump right into inserting Static Meshes, texturing, or lighting. You need to build the framework and test your idea in the editor.

The purpose of BSP is to block out the initial geometry of a level or environment for testing; to [establish scale](https://www.worldofleveldesign.com/categories/ue4/ue4-guide-to-scale-dimensions.php), layout, [flow](https://www.worldofleveldesign.com/categories/level_design_tutorials/one-mistake-in-mirrors-edge.php) and spatial relationship of architecture - for this use BSP brushes.

**BSP brushes are simple, primitive geometric shapes available to use right inside the UE4 editor**. You'll find BSP brushes under **Modes** panel, **Place** tab and **Geometry**:

![img](E:/My%20Drive/0_CSCI_208_GameProgramming_1/0_UnrealBook/images/001-bsp-what-is-it-03.jpg)



---

From Unreal:

https://docs.unrealengine.com/5.0/en-US/geometry-brush-actors-in-unreal-engine/

This document breaks down the use of **Geometry Brushes** in level creation.



```{admonition} Warning
Geometry Brushes are not recommended as a final method of level design. It is not required but can be useful at the early stages of creation.
```





Geometry Brushes are the most basic tool for level construction in Unreal. Conceptually, it is best to think of a Geometry Brush as filling in and carving out volumes of space in your level. Previously, Geometry Brushes were used as the primary building block in level design. Now, however, that role has been passed on to Static Meshes, which are far more efficient. However, Geometry Brushes can still be useful in the early stages of a product for rapid prototyping of levels and objects, as well as for level construction by those who do not have access to 3D modeling tools. This document goes over the use of Geometry Brushes and how they can utilized in your levels.

In general, you can think of Geometry Brushes as a way to create basic shapes for use in your level design process, either as permanent fixtures or as something temporary to test with while your artists finish creating final meshes.

## Uses for Geometry Brushes

While Static Meshes are now primarily used to populate levels with geometry, Geometry Brushes still have their place. Here are some of the typical uses of Geometry Brushes:

### Blocking Out Levels

A standard workflow for developing a level might go something like:

- Block out and path level
- Playtest flow and gameplay
- Modify layout and repeat testing
- Initial meshing pass
- Initial lighting pass
- Playtest for collision and performance issues
- Polish pass