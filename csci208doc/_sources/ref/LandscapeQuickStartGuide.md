# Landscape Quick Start Guide

https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-quick-start-guide-in-unreal-engine

Getting up and running with the basics of the Landscape System in Unreal Engine.

![Landscape Quick Start Guide](https://dev.epicgames.com/community/api/documentation/image/288b48e5-d4fd-4a95-a497-1e0403572d20?resizing_type=fit&width=1920)

The Unreal Editor Landscape Quick Start Guide walks you through creating a new Landscape, sculpting the Landscape, creating new Materials for the Landscape, and painting those Materials on the Landscape.

## 1 - Working with the Landscape Tools

The **Landscape** system inside of Unreal Engine 5 (UE5) is a collection of tools that allow you to create expansive outdoor environments. But before we dive into creating our first Landscape, let us first familiarize ourselves with some of the tools and keyboard inputs that are most commonly used to interact with the Landscape system.

### Opening the Landscape Tool and Working with Modes

All of the tools that are used to interact with the Landscape system can be found under the **Landscape** option that is located in the **Modes** dropdown menu. To enable the Landscape tools, open the Modes dropdown and choose the option from the menu.

The Landscape tool has three modes, **Manage**, **Sculpt**, and **Paint** that are accessible by clicking on their icons at the top of the Landscape's toolbar window. Each mode will allow you to interact with the Landscape in a different manner. Here is a very quick rundown of what each mode allow you to do.

![Landscape Tool Modes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53b43fa2-bd13-441d-a6f5-3641c692f572/01-landscape-tool-modes.png)

| Icon                                                         | Mode            | Description                                                  |
| ------------------------------------------------------------ | --------------- | ------------------------------------------------------------ |
| ![Manage mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29afdfee-835d-48f5-95ac-b7975c692a72/02-landscape-manage-mode.png) | **Manage mode** | Create new Landscapes, and modify Landscape components. Manage mode is also where you work with [Landscape Copy Tool](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-copy-tool-in-unreal-engine) to copy, paste, import, and export parts of your Landscape. For more information about Manage mode, refer to [Landscape Manage Mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-manage-mode-in-unreal-engine). |
| ![Sculpt mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/21dddfc3-f1a8-4f76-aa35-5546aa96ccd3/03-landscape-sculpt-mode.png) | **Sculpt mode** | Modify the shape of your Landscape by selecting and using specific tools. For more information about Sculpt mode, refer to [Landscape Sculpt Mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-sculpt-mode-in-unreal-engine). |
| ![Paint mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a51c5cff-6e06-42c3-bf25-0cc2f2c12ab5/04-landscape-paint-mode.png) | **Paint mode**  | Modify the appearance of parts of your Landscape by painting textures on it, based on the layers defined in the Landscape's Material. For more information about Paint mode, refer to [Landscape Paint Mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-paint-mode-in-unreal-engine). |

### Interacting with the Landscape Tools

While each of the three modes within the Landscape tools allows you to interact with the Landscape differently, but the keyboard and mouse keys that you use are similar. Here is a rundown of some of the most common keys, key combinations, and mouse buttons that are used when working with the Landscape tool.

| **Common Controls**           | **Operation**                                                |
| ----------------------------- | ------------------------------------------------------------ |
| **Ctrl**                      | Allows you to select Landscape components.                   |
| **Left Mouse Button**         | Heightens or increases the heightmap or selected layer's weight. For example, in Sculpting mode, this will raise the Landscape heighmap. In Paint mode this will apply the selected material to the Landscape. |
| **Shift + Left Mouse Button** | Lowers or decreases the heightmap or selected layer's weight. For example, in Sculpting mode, this will lower the Landscape heightmap. In Paint mode, this will erase the selected material that was applied to a particular section of the Landscape. |
| **Ctrl + Z**                  | Undoes last action.                                          |
| **Ctrl + Y**                  | Redoes last undone action.                                   |

## 2 - Creating a new Landscape

### Creating a New FPS Blueprint Project

Before we begin to create our first Landscape, lets create a new project **First Person** Project.

If you are unfamiliar with how to create a new project, check out the following page on [Creating a New Project](https://dev.epicgames.com/documentation/en-us/unreal-engine/level-designer-quick-start-in-unreal-engine).

### Creating a Landscape

1. First, create a new

    

   First Person

    

   project if you have not done so already. While you can use other templates for this tutorial, the First Person will make it a little easier to inspect your Landscape. After choosing the First Person option, click the

    

   Next

    

   button.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7db82718-849c-4d0b-90b6-d8f13596ef7c/05-t-creating-a-new-fps-bp-project-1.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7db82718-849c-4d0b-90b6-d8f13596ef7c/05-t-creating-a-new-fps-bp-project-1.png)

   Click image for full size.

1. Make sure your project is set up to use Blueprints and contains the Starter Content folder. Choose a location where your project will be stored on your computer and make sure it has a proper name. Finally, click the **Create Project** button to continue.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c116ad7-d7e6-4138-82b5-6fdd965d4f11/06-t-creating-a-new-fps-bp-project-2.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c116ad7-d7e6-4138-82b5-6fdd965d4f11/06-t-creating-a-new-fps-bp-project-2.png)

   Click image for full size.

1. Once you have created your new project and the editor has been loaded, create a new level using

    

   File

    

   \>

    

   New Level

    

   and select the

    

   Default

    

   Level from the New Level Template.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f62e1f8c-1175-4a04-ba57-7e5f6f1c7499/07-t-creating-a-new-level.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f62e1f8c-1175-4a04-ba57-7e5f6f1c7499/07-t-creating-a-new-level.png)

   Click image for full size.

1. With your new level now created, select the

    

   Floor

    

   from the level and press the

    

   Delete

    

   key to remove it from the level.

   

   Make sure that you select your player start and move it up slightly in the Z-axis. This will make sure that your player does not start under your newly created Landscape.

   Once completed, you should now have something that looks similar to the following image.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1588b602-b96e-433f-b847-022740a74a0c/08-t-blank-level.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1588b602-b96e-433f-b847-022740a74a0c/08-t-blank-level.png)

   Click image for full size.

1. With the level cleared out and the player start moved up in the Z-axis slightly, it is now time to create a new Landscape. To create a new Landscape, click on the Landscape option in the **Modes** dropdown menu.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42b4639b-3395-4e12-93b2-ec2e9f9eda84/09-t-activating-landscape-mode.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42b4639b-3395-4e12-93b2-ec2e9f9eda84/09-t-activating-landscape-mode.png)

   Click image for full size.

1. Once you have clicked on the Landscape option, you should see the following set of Landscape tools displayed in the **Landscape** panel.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50c7a48b-ce3e-4687-a026-be689f252ce0/10-t-landscape-tools.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50c7a48b-ce3e-4687-a026-be689f252ce0/10-t-landscape-tools.png)

   Click image for full size.

1. For this tutorial, we will just focus on creating a Landscape using the default settings. If you would like to know more about the various settings in the Manage mode of the Landscape tool, please refer to [Creating Landscapes](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-landscapes-in-unreal-engine). For now, make sure that your settings match the image below and then press the **Create** button to create the Landscape.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae8d7038-3f37-4c2e-85f1-54dfb7e7d530/11-t-fillworld-create-landscape.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae8d7038-3f37-4c2e-85f1-54dfb7e7d530/11-t-fillworld-create-landscape.png)

   Click image for full size.

When done, you should have something that looks like this.

[![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3dd062ba-0719-4fcb-9a5a-5983a5813940/12-t-creating-a-new-landscape.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3dd062ba-0719-4fcb-9a5a-5983a5813940/12-t-creating-a-new-landscape.png)

Click image for full size.

## 3 - Sculpting the Landscape

Sculpting the **Landscape** is a time consuming process. All of the tools used for sculpting can be found under the **Sculpt** tab in the Landscape toolbar. If you would like to know more about what each of the Sculpting Tools does in detail, take a look at the [Sculpt Mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-sculpt-mode-in-unreal-engine) page. For quick reference, here is a list of the most common key and mouse interactions that are used when sculpting the Landscape.

| **Common Controls**           | **Operation**                                                |
| ----------------------------- | ------------------------------------------------------------ |
| **Ctrl**                      | Allows you to select Landscape components.                   |
| **Left Mouse Button**         | Heightens or increases the heightmap or selected layer's weight. For example, in Sculpting mode, this will raise the Landscape heighmap. In Paint mode, this will apply the selected material to the Landscape. |
| **Shift + Left Mouse Button** | Lowers or decreases the heightmap or selected layer's weight. For example, in Sculpting mode, this will lower the Landscape heightmap. In Paint mode, this will erase the selected material that was applied to a particular section of the Landscape. |
| **Ctrl + Z**                  | Undoes last action.                                          |
| **Ctrl + Y**                  | Redoes last undone action.                                   |

For this part of the Landscape tutorial, we are going to start with a completely flat section of the Landscape and then build up the details as we go along. The goal here is not to exactly mimic what was created in the tutorial but to get you familiar and comfortable with using the various Landscape tools.



There could be a lot of various reasons as to why what you do in this tutorial does not come out exactly the same as what you see in the following screen shots. Working with the Landscape tools requires a lot of trial and error so your results will vary, sometimes greatly, from what you are seeing in the following set of images. The most important thing to get out of this tutorial is to understand how each of the Landscape tools work and how all the tools work together to give you the final product.

## 

1. To begin, first find a section of the Landscape that you would like to work with. For this tutorial, we are not going to be filling in the entire Landscape but just a section of it. For ease of use, set a camera bookmark by pressing **Ctrl + 1** on the keyboard. This will set a camera bookmark which will make it easier for you to gauge how your Landscape is coming along by giving you a camera view to always come back to. At any time during your editor session, if you press the 1 Key, your camera will be returned to the exact same position that you set.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/71692505-e226-46bf-bc01-9f9ef54f1e9d/13-t-landscape-flat.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/71692505-e226-46bf-bc01-9f9ef54f1e9d/13-t-landscape-flat.png)

   Click image for full size.

1. With the bookmark set, begin painting in the larger details for hills and valleys using the

    

   Sculpt Tool

   . You can find the brush size and strength settings that were used for this step listed below and when completed, you should have something that looks like the following. You can change the value of the Brush Size and Strength either in the Landscape panel or the Landscape toolbar located just above the viewport.

   

   Remember that you use **Left Mouse Button** to raise the Landscape height and **Shift** + **Left Mouse Button** will lower the height of the Landscape.

   | Tool Used  | Brush Size | Strength Setting |
   | ---------- | ---------- | ---------------- |
   | Scupt Tool | 8192       | 0.29             |

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/248998d5-9730-4823-8ad7-67548e68ae36/14-t-landscape-sculpt-tool.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/248998d5-9730-4823-8ad7-67548e68ae36/14-t-landscape-sculpt-tool.png)

   Click image for full size.

1. Once the the hills and valleys are blocked out, it is time to use the

    

   Smooth Tool

    

   to help refine the look and feel of them. Using this tool will smooth your

    

   Landscape

    

   features and make them seem more natural. Be careful not to smooth away all your features! You can find the brush size and strength settings that were used for this step listed below and when completed, you should have something that looks like the following.

   | Tool Used   | Brush Size | Strength Setting |
   | ----------- | ---------- | ---------------- |
   | Smooth Tool | 2048       | 0.29             |

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5dd1d46b-27f9-4e73-92ec-8c218df7a442/15-t-landscape-smooth.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5dd1d46b-27f9-4e73-92ec-8c218df7a442/15-t-landscape-smooth.png)

   Click image for full size.

1. Now that the Landscape is smoothed out, it is time to add some flat mesa like sections using the

    

   Flatten Tool

   . The Flatten Tool captures the height information of the location of your first click and raises/lowers the heightmap to meet that point as you drag around the brush. You can find the brush size and strength settings that were used for this step listed below and when completed, you should have something that looks like the following.

   | Tool Used    | Brush Size | Strength Setting |
   | ------------ | ---------- | ---------------- |
   | Flatten Tool | 2048       | 0.29             |

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0db3b3c0-5def-4a5f-8b16-1992dffe6421/16-t-landscape-flatten.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0db3b3c0-5def-4a5f-8b16-1992dffe6421/16-t-landscape-flatten.png)

   Click image for full size.

1. It is time to use the

    

   Ramp Tool

    

   to add some flat ramps between the mesas. This tool works by designating a start point and an end point for your ramp and then clicking the

    

   Add Ramp

    

   button to create a flat path between the two points. Each point can be moved any direction to create a ramp that fits each unique situation. You can find the brush size and strength settings that were used for this step listed below and when completed, you should have something that looks like the following. If it is not very clear where the Ramp was used, it has been highlighted in yellow.

   | Tool Used | Ramp Width | Side Falloff |
   | --------- | ---------- | ------------ |
   | Ramp Tool | 2000       | 0.40         |

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d80fb2f-cbbb-4b9b-a806-cd528e0580a5/17-t-landscape-ramp.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d80fb2f-cbbb-4b9b-a806-cd528e0580a5/17-t-landscape-ramp.png)

   Click image for full size.

1. Next, we are going to add some erosion effects to the Landscape to give it a weathered look using the

    

   Erosion Tool

    

   which works by simulating erosion done by wind. This tool is perfect for shaving away parts of your hills to create mountain peaks and ridges. You can find the brush size and strength settings that were used for this step listed below and when completed, you should have something that looks like the following.

   | Tool Used    | Brush Size | Strength Setting |
   | ------------ | ---------- | ---------------- |
   | Erosion Tool | 693        | 0.25             |

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f28da47-bc8a-4aef-958a-5a0eb23e1de8/18-t-landscape-erosion.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f28da47-bc8a-4aef-958a-5a0eb23e1de8/18-t-landscape-erosion.png)

   Click image for full size.

1. In the next step, we will take the erosion that was just added in the previous step and push it further by adding some Hydro Erosion to the Landscape. The

    

   Hydro Erosion Tool

    

   is different than the Erosion Tool as it is for simulating how water will erode Landscape details over time. Like the

    

   Smooth Tool

   , be careful not to erode away all your detail. You can find the brush size and strength settings that were used for this step listed below and when completed, you should have something that looks like the following.

   | Tool Used     | Brush Size | Strength Setting |
   | ------------- | ---------- | ---------------- |
   | Hydro Erosion | 2048       | 0.29             |

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5aa1aa15-9222-4b2a-837a-b6dcf7894ced/19-t-landscape-hydro-erosion.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5aa1aa15-9222-4b2a-837a-b6dcf7894ced/19-t-landscape-hydro-erosion.png)

   Click image for full size.

1. To break up the surface of the Landscape even more, we will use the

    

   Noise Tool

   . The Noise Tool adds random noise to the surface of the Landscape by randomly moving the Landscape vertices up or down or both at the same time. You can find the brush size and strength settings that were used for this step listed below and when completed, you should have something that looks like the following.

   | Tool Used  | Brush Size | Strength Setting |
   | ---------- | ---------- | ---------------- |
   | Noise Tool | 2048       | 0.29             |

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e08cbe80-9af0-4b3d-ae62-007b256f305a/20-t-landscape-noise.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e08cbe80-9af0-4b3d-ae62-007b256f305a/20-t-landscape-noise.png)

   Click image for full size.

1. For the final step in the Landscape sculpting part of the tutorial, we will re-use the

    

   Smooth Tool

    

   to help smooth out some of the more jagged areas of the Landscape to give it a more natural look. While you might not need to do this step yourself, this was done to help even out some of the areas that appear too deep or areas that the player might get stuck in if they fall into. You can find the brush size and strength settings that were used for this step listed below and when completed, you should have something that looks like the following.

   | Tool Used   | Brush Size | Strength Setting |
   | ----------- | ---------- | ---------------- |
   | Smooth Tool | 1121       | 0.16             |

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66df2dfd-dae2-4165-9abb-4e2f8c6bba30/21-t-landscape-smooth-cleanup.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66df2dfd-dae2-4165-9abb-4e2f8c6bba30/21-t-landscape-smooth-cleanup.png)

   Click image for full size.

## 4 - Creating Landscape Materials

### Folder Setup

We have finished sculpting the Landscape, it is time to add some Materials to it so that it better resembles something that we see in the real world. But before you do this, you need to first setup some folders to organize the content that you create and migrate into your project.



If you would like to know more about how to setup folders in Unreal Engine 5, please refer to the following page about [Folders](https://dev.epicgames.com/documentation/en-us/unreal-engine/sources-panel-reference-in-unreal-engine).

1. Start by creating a new folder called **Landscape** in your project's **Content** folder.
1. Then inside the Landscape folder, create the following three folders:
   - Materials
   - Resources
   - Textures

When completed, you should have something that looks like the following.

[![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e7e24e1-8585-4f1a-a99e-84f6f7b15960/22-t-landscape-folders.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e7e24e1-8585-4f1a-a99e-84f6f7b15960/22-t-landscape-folders.png)

Click image for full size.

### Migrating Textures

Now that we have the folders in place, it is time to Migrate some Textures from the **Landscape Mountains** learning project so that we have some Textures to work with. This project can be found under the Learn tab in the Epic Games Launcher. If you would like to know more about how to Migrate content from one project to another one, please check out the following page on how to [Migrate Content](https://dev.epicgames.com/documentation/en-us/unreal-engine/sources-panel-reference-in-unreal-engine).



When Migrating content between projects, you could possibly end up with additional folders that you do not want. To fix this, select the Textures that you want inside of the **Content Browser** and then drag them from their current location into the folder that you want them to be placed in. This is purely a house keeping step and will have no impact on the outcome of the tutorial.

You can find the textures located in the following folder located in the Landscapes Content example project.

**/Game/ExampleContent/Landscapes/Textures/**

The Textures that you will be Migrating over from the **Landscape Content Example** project are as follows.

1. **T_LS_Grass_01_D**
1. **T_LS_Grass_01_N**
1. **T_FullGrass_D**
1. **T_FullGrass_N**
1. **T_IceNoise_N**

Once you have the textures migrated over, make sure they are placed in the **Textures** folder that was created in the steps above.

### Creating the Landscape Material

Creating a Material for our Landscape can be done in the following steps.

1. Navigate to the **Materials** folder in the **Content Broswer**.
1. **Right-click** in the **Content Browser** and select **Material** from the **Create Basic Asset** list.
1. Name the newly created Material something that will allow you to easily find it, like **Landscape_Material** for example.



If you have not already done so, please check out the [Materials](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-materials) pages to gain a more in-depth understanding of how materials work inside of Unreal Engine 5.

When this is complete, you will have something that looks like this:

[![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b8c2a98e-45fe-4e56-8125-c6c4e7267213/23-t-landscape-create-new-material.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b8c2a98e-45fe-4e56-8125-c6c4e7267213/23-t-landscape-create-new-material.png)

Click image for full size.

With our new Landscape Material created, open up the Material by **Double-clicking** on it inside of the **Content Browser**. When you do, you should see something like this come up on the screen:

[![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f57071ad-ca31-45f6-9ac3-707658abcb7b/24-t-landscape-blank-material.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f57071ad-ca31-45f6-9ac3-707658abcb7b/24-t-landscape-blank-material.png)

Click image for full size.

It is time to start adding nodes inside of the Material Editor. The first node that you are going to want to create is a **LandscapeLayerCoords** UV node. This node will help to generate UV coordinates that will be used to map the Landscape Material to the Landscape Actor.

[![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c5d6cde-3738-4ab6-b7a6-672cb6fdc215/25-t-landscape-uv-cords.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c5d6cde-3738-4ab6-b7a6-672cb6fdc215/25-t-landscape-uv-cords.png)

Click image for full size.



The quickest way to find nodes specific to Landscape is to search for them in the Materials **Palette** box using Landscape as the key word.

[![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7485f37b-7361-4609-b07f-793ed63681f1/26-t-landscape-material-search.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7485f37b-7361-4609-b07f-793ed63681f1/26-t-landscape-material-search.png)

Click image for full size.

The next Material nodes that we are going to add are going to be for the textures for the ground's **Base Color** and **Normal** maps. For the snow, we are just going to use a **Vector Parameter** (**V + Left-click**) that uses an off White color. To make sure that no **Metallic** information is used, a **Constant** (**1 + Left-click**) of 0 is used and plugged into the **Metallic** input. Finally, for the **Roughness**, we set a **Scalar Parameter** (**S + Left-click**) so that this value can be tweaked via a **Material Instance**. Finally, make sure that you connect the **LandscapeCoords** to the UV's of each of the **Texture Samples**. When completed, your node network should look like this:

[![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5a1e310-1ef4-4595-b7fa-97bea1786f1b/27-t-landscape-material-00.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5a1e310-1ef4-4595-b7fa-97bea1786f1b/27-t-landscape-material-00.png)

Click image for full size.

To add the **Texture Sample** nodes for the various textures, select the desired texture in the **Content Browser** and then press **T + Left-click** in the **Material Editor**'s graph to create the node.



To find more information about these keybindings, take a look at the **Edit > Editor Preferences > Keyboard Shortcuts** window and select the **Material Editor - Spawn Nodes** section.

| **Number** | **Texture Name** |
| ---------- | ---------------- |
| **1**      | T_LS_Grass_01_D  |
| **2**      | T_FullGrass_D    |
| **3**      | T_LS_Grass_01_N  |
| **4**      | T_FullGrass_N    |
| **5**      | T_IceNoise_N     |

After the Material nodes have been added and the **LandscapeCoords** connected to the textures UVs, it is time to add and setup the **Landscape Layer Blend** node. The **Landscape Layer Blend** node allows for the blending of layers via Weight blending, Height blending, or Alpha blending. Weight blending uses each layer's painted weight to determine which to display. We use Weight blending where we want two surfaces to blend seamlessly into each other, such as rock into sand. Height blending uses the same weight information along with an additional height value taken from the Texture Sample's Alpha channel and is best used when one material needs to clearly sit on top of another, such as the Grass and Snow sitting on top of the Soil layer. Finally, Alpha blending uses the painted weight information with an Alpha layer to determine the final result.

The following table shows what **Textures** are associated with which **Layer Name** and what **Blend Type** they use.



When you first place down a **Landscape Layer Blend** node, it will be blank like in the image below labeled one. To add **Layers**, you need to select the node in the **Material Graph** and then in the **Details** panel, click on the **Plus** icon that is in-between the word **Elements** and the **Trash Can** icon. This icon is highlighted yellow in the image labeled two. How many textures you are using will determine how many Layers you will want to have.

![Landscape node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87ca24c3-7c13-4a69-8b18-fc251cdee0b4/28-t-landscape-mlb-node.png) ![Landscape adding layers to node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60c5eb92-cf8b-41e8-9a5a-8a39e45c39f9/29-t-landscape-adding-layers-to-mlb-node.png)

**Layer Blend Base Color**

| **Texture**        | **Layer Name** | **Blend Type**  | **Preview Weight** |
| ------------------ | -------------- | --------------- | ------------------ |
| T_LS_Grass_01_D    | Soil           | LB Weight Blend | 1.0                |
| T_FullGrass_D      | Grass          | LB Height Blend | 0.0                |
| Snow as a Vector 3 | Snow           | LB Height Blend | 0.0                |

[![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e85a5591-aa29-4901-9755-fb7431e6e47e/30-t-landscape-layer-blend-bc.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e85a5591-aa29-4901-9755-fb7431e6e47e/30-t-landscape-layer-blend-bc.png)

Click image for full size.

**Layer Blend Normal**

| **Texture**     | **Layer Name** | **Blend Type**  | **Preview Weight** |
| --------------- | -------------- | --------------- | ------------------ |
| T_LS_Grass_01_N | Soil           | LB Weight Blend | 1.0                |
| T_FullGrass_N   | Grass          | LB Height Blend | 0.0                |
| T_IceNoise_N    | Snow           | LB Weight Blend | 0.0                |

[![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d68f679-74b7-4d3e-9a31-06e54065bcea/31-t-landscape-layer-blend-n.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d68f679-74b7-4d3e-9a31-06e54065bcea/31-t-landscape-layer-blend-n.png)

Click image for full size.



For more in-depth information about using the **Landscape Layer Blend** node or to troubleshoot any issues, please read the [Terrain Expressions](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-material-expressions-in-unreal-engine) page.

Once the **Layer Blend** nodes have been set up, it is time to connect the Texture maps to them. Height blended materials will have both a Layer connection and a Height connection to accommodate the need for the additional height information. When completed, you should have something that looks like the following.

[![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3bfaacd1-3f3a-4de7-9b5a-b9114afa24b4/32-t-landscape-material-final.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3bfaacd1-3f3a-4de7-9b5a-b9114afa24b4/32-t-landscape-material-final.png)

Click image for full size.



The material connections were colored in Photoshop to help better illustrate where everything needed to be connected. Currently there is no way to change the color of lines connecting Material nodes inside of Unreal Engine 5.

## 5 - Painting Landscape Materials

With the Landscape material created, it is time to apply the Material to the Landscape and begin using the Paint tools.

### Landscape Painting Prep

Before we can begin painting the Landscape, there is some setup that needs to be done first. Start by applying your Landscape Material to the Landscape:

1. Find your Material in the **Content Browser**. This should be located under a folder labeled **Materials** that was created in the previous section. Click on it so that it is selected.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/abc9d681-476b-48e3-90f4-07c1d8ed3581/33-t-landscape-materail-in-cb.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/abc9d681-476b-48e3-90f4-07c1d8ed3581/33-t-landscape-materail-in-cb.png)

   Click image for full size.

1. With the Landscape Material selected in the **Content Browser**, select the Landscape in the world. Then in the **Details** panel, expand the **Landscape** section and look for the **Landscape Material** input.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d05dd0d4-4225-4473-beff-c49fc5020fa3/34-t-landscape-material-input.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d05dd0d4-4225-4473-beff-c49fc5020fa3/34-t-landscape-material-input.png)

   Click image for full size.

1. Apply the Material to the Landscape using the

    

   Use Selected Asset from the Content Browser

    

   arrow icon. You can also drag the Material asset from the

    

   Content Browser

    

   to the

    

   Details

    

   panel and drop it on the

    

   Landscape Material

    

   input.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6505fbdb-8c7f-41dc-a38b-2be12d0d577a/35-t-landscape-assign-material.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6505fbdb-8c7f-41dc-a38b-2be12d0d577a/35-t-landscape-assign-material.png)

   Click image for full size.

1. When completed, you should have something that looks like this:

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13025827-fcdc-4adb-bcd8-1ba5817fe59d/36-t-landscape-with-material-applied.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13025827-fcdc-4adb-bcd8-1ba5817fe59d/36-t-landscape-with-material-applied.png)

   Click image for full size.

   

   If you see black lines in your Landscape, they come from having Un-Built lighting. If you re-build your level's lighting, the black lines will go away.

Now that the Landscape Material is applied, it is almost time to stat painting but before we can do that, we must first create and assign three **Landscape Layer Info Objects**. If you try to paint before you assign the **Landscape Layer Info Objects**, you will get the following warning message.

[![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2bae1bea-33f5-418b-b82b-b35280a40e38/37-t-landscape-paint-warning.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2bae1bea-33f5-418b-b82b-b35280a40e38/37-t-landscape-paint-warning.png)

Click image for full size.

You need to create three **Landscape Layer Info Objects**, one for each Texture that you want to paint. Here is how you do it:

1. First, make sure that you are in **Landscape Paint** mode.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a596b1c-6813-4e65-b603-b522783fb8a5/38-t-landscape-paint-mode.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a596b1c-6813-4e65-b603-b522783fb8a5/38-t-landscape-paint-mode.png)

   Click image for full size.

1. In the Landscape panel, under the **Target Layers** section, you should see three inputs labeled **Soil, Grass,** and **Snow**.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/187a745c-dab2-47e0-a860-39d611f74fbd/39-t-landscape-target-layers.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/187a745c-dab2-47e0-a860-39d611f74fbd/39-t-landscape-target-layers.png)

   Click image for full size.

1. To the right of the names, there is a **Plus Sign** icon. Clicking that will bring up another menu that will ask what type of layer you would like to add. For this example, pick the **Weight-Blended Layer (normal)** option.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48b5088e-cece-44fb-8e9c-6bc3b71d111e/40-t-landscape-blend-layer.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48b5088e-cece-44fb-8e9c-6bc3b71d111e/40-t-landscape-blend-layer.png)

   Click image for full size.

1. When you select the **Weight-Blended Layer (normal)** option, you will be prompted with a pop-up box that is asking you where you want to save the newly created **Landscape Layer Info Objects**. Select the **Resources** folder that is under the **Landscape folder** and then press the **OK** button.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/119a7261-df7a-47fa-9d83-9e1d4d412f28/41-t-landscape-layer-info-save.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/119a7261-df7a-47fa-9d83-9e1d4d412f28/41-t-landscape-layer-info-save.png)

   Click image for full size.

1. Once you have completed the first one, repeat the same process for the other two. You should have something that looks like the following:

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54ab09cb-6ede-4273-ace8-2a4923c24d98/42-t-landscape-finshed-layers.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54ab09cb-6ede-4273-ace8-2a4923c24d98/42-t-landscape-finshed-layers.png)

   Click image for full size.

Now with the **Landscape Layer Info Objects** created and applied, we can begin to paint our Landscape.

### Painting the Landscape

Before you begin to paint the Landscape, here is a re-cap of some of the most used commonly used keyboard and mouse inputs that you will use when painting the Landscape.

| **Common Controls**   | **Operation**                                                |
| --------------------- | ------------------------------------------------------------ |
| **Left Mouse Button** | Performs a stroke that applies the selected tool's effects to the selected layer. |
| **Ctrl+Z**            | Undo last stroke.                                            |
| **Ctrl+Y**            | Redo last undone stroke.                                     |

The main tool that you will use for applying textures to your Landscape is going to be the **Paint Tool**. To find out more about all of the tools that you can use to paint on the Landscape, check out the [Paint Mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-paint-mode-in-unreal-engine) documentation.

To apply a Material to the Landscape, press and hold the **Left Mouse Button** to apply whatever you have selected to the area under the brush.

To select a new texture to paint, make sure you are in **Landscape Painting Mode** then under the **Target Layers** section, select which texture you want to paint with by clicking on it in the list. Whichever texture is highlighted will be painted on the Landscape. In the image below, you can see the **Soil** layer is highlighted meaning that this is the texture that will be painted to the Landscape.

[![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01cb201a-048f-422f-9577-904f0bafaf6c/43-t-landscape-picking-layers-to-paint.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01cb201a-048f-422f-9577-904f0bafaf6c/43-t-landscape-picking-layers-to-paint.png)

Click image for full size.

When you finish painting, you should have something that looks like this.

[![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/207dc6dc-b7d4-499c-bde3-8f0c23f046e0/44-t-landscape-final-paint.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/207dc6dc-b7d4-499c-bde3-8f0c23f046e0/44-t-landscape-final-paint.png)

Click image for full size.

### Possible Issues and Workarounds

When you first start painting on your Landscape you might run into an issue where the base Material disappears or turns black, like in the following picture:

[![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c47730b-4003-4014-b507-a5bb57c0ae9b/45-t-first-paint-issues.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c47730b-4003-4014-b507-a5bb57c0ae9b/45-t-first-paint-issues.png)

Click image for full size.

This happens when there is no Paint Layer data on the Landscape when you first start to paint. To fix this issue, continue to paint over the Landscape generating the Paint Layer data as you go. If you would like to fill in the entire Landscape, first select a large brush size, like 8192.0, pick a layer that you want to use as a base and paint over the entire Landscape once. This will create Paint Layer data and allow you to continue to paint without anything turning black.

Another issue that you might run into is that the scale of the Textures on your Landscape are either too big or too small. To fix this, open your Landscape Material and select the **Landscape Coords** node. With that node selected, adjust the **Mapping Scale** in the **Details** panel and save the Material. Once the Material is re-compiled, check the scale out in the viewport. If the scale is not to your liking, then repeat the processes above until you get the results you want.

[![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/febdd501-3f95-4c8d-a113-9b8b116e8e94/46-t-landscape-texture-size.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/febdd501-3f95-4c8d-a113-9b8b116e8e94/46-t-landscape-texture-size.png)

Click image for full size.

Here is a comparison between a **Mapping Scale** of **0.5** on the Left and **5.0** on the Right.

![Mapping Scale: 0.5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7982cbba-80ac-4da5-8b0f-8b756391d78d/47-mapping-scale-0-5.png)

![Mapping Scale: 5.0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bdda0b4a-a2ab-4af7-844e-3710f8a640bb/48-mapping-scale-5-0.png)

Mapping Scale: 0.5

Mapping Scale: 5.0

## 6 - Landscape Tips and Tricks

While the quick start tutorial above will get you up and running with a Landscape, it barely scratches the surface of what the Landscape tools can do. This section aims to show you some tips and tricks for using the Landscape Tool as well as some external tools that you can use to generate your Landscape.

### Tips & Tricks

- When using the **Paint Tools**, you might find it easier to paint over what you would like to erase than to try and erase it using **Shift** + **Left Mouse Button**.

- When using the **Alpha Brush**, remember that you can change what the pattern that the brush uses by selecting a different RGB channels from the **Texture Channel** drop down menu. This is very handy because you can pack up to three different Alpha patterns in a single texture.

  [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09274472-98ac-4cd3-ba16-df89b2eafae2/49-t-landscape-tips-tricks-00.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09274472-98ac-4cd3-ba16-df89b2eafae2/49-t-landscape-tips-tricks-00.png)

  Click image for full size.

- Landscape compiles shaders separately for each component based on which layers are painted on them. For example, if you have a component with a dirt layer on it but no trace of the grass layer has been painted on it, the textures for the grass layer are left out of the material for that component, making it cheaper to render. So when you do an optimization pass, it can be worthwhile to go over a Landscape and look for components that only have a tiny trace of a given layer and erase them to reduce material complexity.

- Another issue to watch out for when painting layers is to avoid having too many textures on one component. The material editor stats show the limit of how many texture samples you are allowed to use, but for Landscape materials the masks for each layer count as texture samples too and do not show in the stats. If a component starts showing the default texture (Grey Squares) when you paint a new layer onto it, it is likely that it is gone over the texture sample limit and either needs to have a layer erased or the material needs to be optimized to use less textures.

- You can change the LOD Distance Factor for individual Landscape components so they will simplify at closer or further distance thresholds. Things like mountain peaks or anything with a distinct silhouette will LOD most noticeably as you move further away, so you can reduce the LOD bias for those components to preserve their shape. You can also raise the LOD bias for low-detail areas like flat plains that will not look noticeably different with less tessellation.

### World Composition

Unreal Engine 5 (UE5) now offers the ability to create massive worlds made using Landscape that can easily be managed by using the **World Composition** tool. World Composition was designed to help simplify the management of large worlds, especially if those worlds are made using the Landscape system. To find out more about the World Composition tool, please refer to the official document that you can find here:

[World Composition Documents](https://dev.epicgames.com/documentation/en-us/unreal-engine/world-composition-in-unreal-engine)

### External Creation Tools

While the default Landscape tools do have the ability to meet all of your sculpting and painting needs, there could be some situations where you might want some extra control over your Landscape's look and feel. The following is a list of software packages that could help you obtain the results you are looking for if you cannot get them from using the Landscape tools.

|                                                            |                                                              |
| ---------------------------------------------------------- | ------------------------------------------------------------ |
| [Houdini](https://www.sidefx.com/)                         | Procedural terrain generation in Houdini uses a collection of heightfield nodes to let you use layer shapes and add noise to define the look of your digital landscapes. Use advanced erosion tools for more control over details such as fluvial lines, river banks, debris, and new hierarchical scattering for more efficient placement of elements into landscapes. You can then export height and/or mask layers to create terrain in UE5, or you can wrap up your terrain networks into Houdini Digital Assets that will open up in UE5 using the Houdini Engine plug-in. When Digital Assets include heightfield nodes, they will integrate seamlessly with Unreal Engine's native Terrain tools. |
| [Mudbox](http://www.autodesk.com/products/mudbox/overview) | While primarily a tool for digital sculpting and painting 3D meshes, Mudbox can also be used to generate heightmap data for your Landscape. You can read more about how Mudbox might be able to help you out with your Landscape by checking out their website. |
| [Terragen](http://planetside.co.uk/)                       | Terragen is another powerful fully procedural terrain creation software. Much like World Machine, it can be used to build, texture, and export both heightmaps and textures for your Landscape. You can read more about how Terragen might be able to help you out with your Landscape by checking out their website. |
| [World Machine](http://www.world-machine.com/)             | World Machine is a powerful procedural terrain creation software. It can be used to build, texture, and export both heightmaps and textures for your Landscape. You can read more about how World Machine might be able to help you out with your Landscape by checking out their website. |
| [ZBrush](http://pixologic.com/)                            | Zbrush is another digital sculpting and painting tool that can be used to generate heightmap data for your Landscape. You can read more about how Zbrush might be able to help you out with your Landscape by checking out their website. |

[landscape](https://dev.epicgames.com/community/search?query=landscape)[building virtual worlds](https://dev.epicgames.com/community/search?query=building virtual worlds)[open world](https://dev.epicgames.com/community/search?query=open world)