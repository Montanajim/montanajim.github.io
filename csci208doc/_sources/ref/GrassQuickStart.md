# Grass Quick Start

Learn how to add Grass textures to a landscape.

![Grass Quick Start](https://dev.epicgames.com/community/api/documentation/image/f3985504-b0fd-4300-bc8a-1dae2e3dd380?resizing_type=fit&width=1920)

## Overview

In this Quick Start guide, we will take a look at how you can set up and apply a grass texture to a landscape. Over the course of this Quick Start tutorial you will learn how to create, set up, and spawn static meshes to make your Landscape appear covered in thick grass. You will be introduced to key properties and settings that will help you shape your virtual grasslands to fit your project's needs.

[![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c29302d-e1db-4862-af6f-c744b88fea28/01-t-grass-intro.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c29302d-e1db-4862-af6f-c744b88fea28/01-t-grass-intro.png)

Click image for full size.

You will also learn about the Actors and properties required for a grassy-looking result to function correctly and deliver the results you want. When you have completed this Quick Start, you will have a new level that should look similar to the image above.



Currently, the Grass system will only work with the Landscape Terrain Actor. Trying to use the Grass system to spawn grass on any other Actor type will not work.

## 1 - Prerequisites

Download the **Open World Demo Collection** content pack as some of the content from the collection will be used in the following Quick Start. Once the Open World Demo Collection is downloaded, add it to the project that you are using to follow along with this Quick Start by doing the following:

1. From the Epic Games Launcher in either the **Learn** or **Marketplace** tab, locate and then download the **Open World Demo Collection**.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8094227b-76b5-4359-beab-22e0bf12c6bf/02-owdc-1.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8094227b-76b5-4359-beab-22e0bf12c6bf/02-owdc-1.png)

   Click image for full size.

1. Go the the **Library** section of the launcher and under **Vault** section locate the Open World Demo Collection.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2c1a46e-cf67-43ee-9cc3-ca2d616c9d2c/03-owdc-2.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2c1a46e-cf67-43ee-9cc3-ca2d616c9d2c/03-owdc-2.png)

   Click image for full size.

1. Click on the **Add to Project** button.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0e3305c-e1de-4201-8ee3-f429a7e8e59c/04-add-to-project.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0e3305c-e1de-4201-8ee3-f429a7e8e59c/04-add-to-project.png)

   Click image for full size.

1. A list of projects that you can add this to will appear. Select the project that you are using to follow along with this Quick Start and then press the **Add to Project** button.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0961fb8-0a60-4c0c-81c6-896dd4328845/05-select-project.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0961fb8-0a60-4c0c-81c6-896dd4328845/05-select-project.png)

   Click image for full size.

## 2 - Initial Level Setup

Now, we will create a new level and Landscape terrain so that we have something on which to apply the grass.

1. Create a new level that uses the blank **Default** template as a base.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/402737ac-513d-4141-b356-fa924dec85ea/06-t-new-level.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/402737ac-513d-4141-b356-fa924dec85ea/06-t-new-level.png)

   Click image for full size.

1. Add a new Landscape Actor to the level. In the Main Toolbar, click the **Modes** button, and select **Landscape** to display the Landscape panel and toolbar, and then click on the **Create** button.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67717655-15e4-4823-ab21-52a2fe092869/07-create-landscape.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67717655-15e4-4823-ab21-52a2fe092869/07-create-landscape.png)

   Click image for full size.

1. To help better show off the Grass Tool, we are going to add a some noise to our Landscape terrain so it is not completely flat. In the **Landscape** toolbar **Sculpt** tab, click **Noise** from the tool list. Set the Noise properties with the following values.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da42f043-8e37-44d0-8de7-49f1ae78c427/08-t-sculpt-tool-settings.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da42f043-8e37-44d0-8de7-49f1ae78c427/08-t-sculpt-tool-settings.png)

   Click image for full size.

   | Property Name     | Value   | Additional Details                                           |
   | ----------------- | ------- | ------------------------------------------------------------ |
   | **Brush Size**    | 65536.0 | This gives us a brush that is big enough to effect the entire Landscape terrain at once. |
   | **Tool Strength** | 0.01    | Since we only want a very subtle effect, set the Tool Strength very low and add more intensity by painting more. |
   | **Noise Scale**   | 256     | Making the Noise Scale bigger makes the noise look smoother and more natural when applied to the Landscape. |

1. Position the Landscape Brush in the viewport so that it covers the entire Landscape terrain. Click the Left Mouse Button **3** to **4** times to add some very subtle noise to the Landscape terrain.

1. Exit Landscape mode. Click the **Modes** button, and choose **Select** to display the **Place Actors** panel.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/082ecc19-3009-437f-8ed2-23e8165a60e0/09-place-actors.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/082ecc19-3009-437f-8ed2-23e8165a60e0/09-place-actors.png)

   Click image for full size.

   When completed, you should have something that looks similar to the following image.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff32f837-5e6d-430e-a37e-895b5d0beb6d/10-t-noise-on-landscape.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff32f837-5e6d-430e-a37e-895b5d0beb6d/10-t-noise-on-landscape.png)

   Click image for full size.

   

   The Grass system works on a completely flat Landscape terrain. The above modification to the Landscape was done purely for artistic reasons, to help show the final result.

## 3 - Grass Tool Actor Creation and Setup

We will create the required Actors and Materials the Grass Tool needs to function correctly. We will continue to work with the the level that was created in the last step.

1. Create a Landscape Grass Type: **right-click** in the **Content Browser**. From the displayed context menu, go to **Foliage** > **Landscape Grass Type** and name it **Grass_00**.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6ddd84c-7402-4e6e-b7d5-9fe13a189ba5/11-t-create-ls-grass.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6ddd84c-7402-4e6e-b7d5-9fe13a189ba5/11-t-create-ls-grass.png)

   Click image for full size.

1. Open up the Landscape Grass Type and add a new item to the **Grass Varieties** array: **double-click** on **Landscape Grass Type** and once opened, press the **Plus** icon that is to the right of the **Grass Varieties** name.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9cbc4ca-b839-4763-884d-88f40f71adad/12-t-add-new-gv.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9cbc4ca-b839-4763-884d-88f40f71adad/12-t-add-new-gv.png)

   Click image for full size.

1. Inside of the **Landscape Grass Type** Actor look for the **Grass Mesh** section, click on the input box that says **None** and enter **SM_FieldGrass_01** as the search term, then click on the **SM_FieldGrass_01** to load it as the **Grass Mesh**.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77df16e0-e277-4177-b1ff-c62d8eda9775/13-t-set-grass-type.gif)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77df16e0-e277-4177-b1ff-c62d8eda9775/13-t-set-grass-type.gif)

   Click image for full size.

1. With the Static Mesh added we need to set the following properties to ensure that we are spawning enough grass mesh and that those meshes are randomly rotated and aligned to the Landscape terrain.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2ac45364-8bb1-4bfe-8371-0f9f062e5f80/14-t-grass-props.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2ac45364-8bb1-4bfe-8371-0f9f062e5f80/14-t-grass-props.png)

   Click image for full size.

   | Property Name        | Value   | Additional Details                                           |
   | -------------------- | ------- | ------------------------------------------------------------ |
   | **Grass Density**    | 400.0   | Because we want this to look like grass, we must spawn a lot of Static Meshes to make the Landscape appear densely covered in grass. |
   | **Use Grid**         | Enabled | To make the Static Meshes look more naturally placed, this offset is their placement position. |
   | **Random Rotation**  | Enabled | Giving the Static Meshes used for the plants and grasses a random rotation makes sure that the same side of the Static Mesh used is not seen all the time, adding to the visual variety of the scene. |
   | **Align to Surface** | Enabled | This makes sure that the Static Mesh used conforms to the surface of the Landscape terrain. |

## 4 - Landscape Materials and the Grass Tool

Before we can begin to use the Grass Tools we first have to create a Material that can work with both the Landscape terrain and the **Landscape Grass Type**. We will cover how to set up this Material, as well as how to link it so that it will work with the Landscape Grass Type.



If you would like to have a more in-depth look at how the Landscape terrain works in UE5, refer to the [Landscape](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-outdoor-terrain-in-unreal-engine) pages for more information.

1. Create a new Material for our Landscape Terrain by **right-clicking** in the **Content Browser**, then selecting the **Material & Textures** option from the **Create Basic Asset** section, and name the new Material, **MAT_GT_Grass**.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e2ead98-470a-4c4d-add6-616cd05b091a/15-t-create-new-material.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e2ead98-470a-4c4d-add6-616cd05b091a/15-t-create-new-material.png)

   Click image for full size.

1. Open up the **MAT_GT_Grass** Material by **double-clicking** on the Material inside of the **Content Browser**, then add the following two Textures from the **Open World Demo Collection** to the Material Graph.

   - **T_AlpinePatch001_D_alt_R**
   - **T_GDC_Grass01_D_NoisyAlpha**

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/167f01d9-09f8-47d1-b8bc-fabdf3dfc309/16-t-added-textures.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/167f01d9-09f8-47d1-b8bc-fabdf3dfc309/16-t-added-textures.png)

   Click image for full size.

1. Using the **Palette** search function, search for the Material Expression nodes listed below. Once you locate a required Material Expression node, select it in the Palette and then drag it into the Material Graph.

   | Material Expression Name   | Amount | Additional Details                                           |
   | -------------------------- | ------ | ------------------------------------------------------------ |
   | **Landscape Layer Blend**  | 1      | To make the Landscape terrain look more realistic you will often need to blend and paint multiple together or separately and that is what the Landscape Layer Blend allows you to do. |
   | **Landscape Layer Sample** | 1      | This Material Expression allows the Material and the Landscape to talk to one another to ensure the right Static Mesh is used whenever a certain Landscape layer is painted. |
   | **Landscape Grass Output** | 1      | This enables the Landscape terrain to be able to spawn the Grass Types based on the setup in the Landscape Material. |

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e078a9b-225d-4986-9fd1-0b4f87b5f622/17-t-add-material-nodes.gif)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e078a9b-225d-4986-9fd1-0b4f87b5f622/17-t-add-material-nodes.gif)

   Click image for full size.

   

   If you are unfamiliar with how the UE5 Material Editor works or would just like more information about it, check the official **[Unreal Engine Material documentation](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-materials)** for more information on all things related to Materials.

1. Select the **Landscape Layer Blend** node and under the **Details** panel in the **Layers** section and add two new Layers to it by clicking the **Plus** icon 2 times.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2752c6c3-08e6-4a1e-88c3-4c494a5366ff/18-t-lb-add-2-layers.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2752c6c3-08e6-4a1e-88c3-4c494a5366ff/18-t-lb-add-2-layers.png)

   Click image for full size.

1. Once 2 layers have been added, set the **Layer Name** of one to **Grass** and set the **Layer Name** of the other one to **Rock** also setting the **Preview Weight** to **1.0** for each.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/388d4ea4-8c2c-4bef-a3d5-d950d6b30a3f/19-t-ls-layer-blend-setup.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/388d4ea4-8c2c-4bef-a3d5-d950d6b30a3f/19-t-ls-layer-blend-setup.png)

   Click image for full size.

1. Connect the **T_AlpinePatch001_D_alt_R** Texture to the **Layer Rock** input on the **Landscape Layer Blend** node then connect the **T_GDC_Grass01_D_NoisyAlpha** to the **Layer Grass** input finally connect the **Output** of the **Landscape Layer Blend** node into the **Base Color** input on the Main Material Node, **Mat_GT_Grass**.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6f4339a-871d-4d48-9133-390cbb68f646/20-t-hook-up-textures.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6f4339a-871d-4d48-9133-390cbb68f646/20-t-hook-up-textures.png)

   Click image for full size.

1. In the **Content Browser**, select the **Grass_00** Landscape Grass Type that was created in the last step.

1. In the **Material** under the **Grass Type** option, press the **Arrow** icon to load the Actor that is currently selected in the Content Browser.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c4ebbacf-fab6-4e25-bd0e-0e73784a8b46/21-t-input-grass-type.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c4ebbacf-fab6-4e25-bd0e-0e73784a8b46/21-t-input-grass-type.png)

   Click image for full size.

1. Select the **Landscape Layer Sample** node under the **Parameter Name** input **Grass** for the name and connect the Output from the **Landscape Layer Sample** to the input of the **Landscape Grass Output** node.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0347fa2e-1586-43a2-857e-1783c977c677/22-t-llw-setup.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0347fa2e-1586-43a2-857e-1783c977c677/22-t-llw-setup.png)

   Click image for full size.

1. When completed you should have a Material that looks like the following. As always, do not forget to press the **Apply** and **Save** buttons to compile and save the Material.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f0cc827-2143-4aa2-a44a-efc90213b581/23-t-final-material.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f0cc827-2143-4aa2-a44a-efc90213b581/23-t-final-material.png)

   Click image for full size.

## 5 - Using the Grass Tools

In order to see the Grass system in action, we need to apply the Material that was created in the last step to the Landscape and then use the Landscape painting tools to define where we want the grass to be spawned. In the following section, we will go over how to apply our Material to the Landscape Terrain, then how to use the Landscape Painting Tools to define areas where grass should spawn. We will continue to work in the level that was created in the last step.

1. Select the Landscape Actor that was placed in the level by clicking on it in the viewport.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94978993-38c2-48bf-bbf0-9c9edd442e35/24-t-selected-landscape.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94978993-38c2-48bf-bbf0-9c9edd442e35/24-t-selected-landscape.png)

   Click image for full size.

1. Locate the **MAT_GT_Grass** Material in the **Content Browser** and click on it to select it.

1. On the Landscape Terrain under the **Details** panel in the **Landscape Material** section, press the **Arrow** icon to apply the **MAT_GT_Grass** Material to the Landscape Terrain.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6840490-86db-494e-9e25-20ec2a2a32f8/25-t-apply-material.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6840490-86db-494e-9e25-20ec2a2a32f8/25-t-apply-material.png)

   Click image for full size.

1. In the **Main Toolbar**, click the **Modes** button, select **Landscape** mode. From the **Landscape** toolbar, click on the **Paint** tab to go into **Paint** mode.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/411e8a98-c24c-47d5-9e3c-184dc6944cb9/26-t-landscape-paint-mode.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/411e8a98-c24c-47d5-9e3c-184dc6944cb9/26-t-landscape-paint-mode.png)

   Click image for full size.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aad043f5-d9c4-4523-8bfc-51b67fd861d5/27-t-landscape-paint-mode-1.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aad043f5-d9c4-4523-8bfc-51b67fd861d5/27-t-landscape-paint-mode-1.png)

   Click image for full size.

1. Under the **Target Layers** section, add a new **Layer Info** by pressing the **Plus** icon on the far right of the layer name.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5fa510bf-7877-43f8-ac41-a89dc233e570/28-t-add-target-layers.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5fa510bf-7877-43f8-ac41-a89dc233e570/28-t-add-target-layers.png)

   Click image for full size.

1. When prompted, select the **Weight-Blended Layer (normal)** option, then select a location to save the new Layer Blend in the Content Browser. Make sure that you create **Layer Info** for both the Rock and the Grass.

1. Select the **Grass** Target Layer, then hold down the **Left Mouse Button** inside the viewport to begin painting the Grass Material to the Landscape Terrain. For this step, try to completely cover the Landscape, giving you results that look like this.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2555563f-01cd-4db2-9222-fdca4c785147/29-t-painting-grass-2.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2555563f-01cd-4db2-9222-fdca4c785147/29-t-painting-grass-2.png)

   Click image for full size.

   

   Depending on the power of your development PC, when you start to paint on the Landscape the editor might become unresponsive as the grass is spawned. This is normal behavior as the grass is dynamically spawned after you have finished painting. Turning down the **Grass Density** in the **Landscape Grass Type** while working, then putting it back up to the desired level when done, is a great way to help mitigate this as much as possible.

1. To remove grass from the Landscape Terrain, select the Rock Target Layer then inside of the viewport hold down the **Left Mouse button** to begin replacing the grass Texture with the rock Texture.

   <iframe src="https://dev.epicgames.com/community/api/cms/videos/V_PpukpG/embed.html" style="box-sizing: border-box; border: 0px; top: 0px; left: 0px; width: 632.008px; height: 355.502px;"></iframe>

   Adjusting the **Brush Size** and **Tool Strength** will help to better define how the grass is placed or removed while painting on the Landscape.

## 6 - On Your Own

Now that you have seen the power that the Grass tool offers, try using the tools listed below in conjunction with what you have just learned to make a level that looks like the following image:

![On Your Own](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5231b3b-73c5-44ca-8799-35cf69c597a9/44-t-on-your-own.png)

- Use the [Procedural Foliage Tool](https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-foliage-tool-in-unreal-engine) Tool to make the Landscape look like it is densely covered in grass, flowers and bushes.
- Define the look and feel of the Landscape terrain using the **[Landscape Sculpt](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-sculpt-mode-in-unreal-engine)** tools to add features such as hills, mountains and lakes.
- Give the surface of the Landscape more visual variety and detail by creating a [Landscape Material](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-materials-in-unreal-engine) that has multiple Textures that can be painted on the Landscape terrain.
- Adjust the **[Directional Light](https://dev.epicgames.com/documentation/en-us/unreal-engine/directional-lights-in-unreal-engine)** to make the level lighting resemble lighting that happens in the early morning or late afternoon.
- Set up the level lighting to use a completely dynamic based lighting solution that will make use of dynamic shadows as well as **[Ray Traced Distance Field Soft Shadows](https://dev.epicgames.com/documentation/en-us/unreal-engine/distance-field-soft-shadows-in-unreal-engine)**.
- Try using the [Foliage System](https://dev.epicgames.com/documentation/en-us/unreal-engine/foliage-mode-in-unreal-engine) tools to remove or tweak the placement, rotation and scale of the Foliage meshes that are placed by the Procedural Foliage tool so that you can get the exact look you are going for.
- Show off your creation to others by using a [Camera](https://dev.epicgames.com/documentation/en-us/unreal-engine/camera-actors-in-unreal-engine) in conjunction with [Sequencer](https://dev.epicgames.com/documentation/en-us/unreal-engine/real-time-compositing-with-sequencer-in-unreal-engine) to render out a video of your level for you to share with the world.

[landscape](https://dev.epicgames.com/community/search?query=landscape)[building virtual worlds](https://dev.epicgames.com/community/search?query=building virtual worlds)[open world](https://dev.epicgames.com/community/search?query=open world)