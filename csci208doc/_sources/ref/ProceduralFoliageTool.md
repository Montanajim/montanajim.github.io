# Procedural Foliage Tool

How to set up and use the Procedural Foliage tool.

![Procedural Foliage Tool](https://dev.epicgames.com/community/api/documentation/image/2adb8162-0488-493d-a99d-6a5d16c900d2?resizing_type=fit&width=1920)

In this Quick Start tutorial we will take a look at how the **Procedural Foliage Tool** works. Over the course of this Quick Start tutorial you will learn how to create, set up, and spawn an entire forest's worth of trees inside of UE5 using only the Procedural Foliage tool. You will also be introduced to key properties and settings that will help you shape your virtual forest to fit your project's needs.

![Final Product](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84be3a72-c9d8-4f7f-acc1-5fea8002bd05/01-t-pf-qs-final-product.png)

You will also be exposed to all of the required Assets and properties the Procedural Foliage tool requires to function correctly and deliver the results you want. When you have completed this Quick Start you will have a new level that should look similar to the image above.

### Prerequisites

Before you can use the Procedural Foliage tools in your project, you must first enable them by doing the following.

1. From the **Main Menu** open the **Edit** menu then click on **Editor Preferences**.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91ecdb9c-7351-4cd5-8dd0-0858463c56f5/02-pfs-editor-prefs.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91ecdb9c-7351-4cd5-8dd0-0858463c56f5/02-pfs-editor-prefs.png)

   Click image for full size.

1. Inside of the Editor Preferences **right - click** on the **Experimental** section.

1. Enable the Procedural Foliage option by clicking on the checkmark box next to the word **Procedural Foliage**.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f5e76f4d-3470-4abb-8929-f136e3bc26aa/03-pfs-editor-preferences.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f5e76f4d-3470-4abb-8929-f136e3bc26aa/03-pfs-editor-preferences.png)

   Click image for full size.

You will also need to download the **Open World Demo Collection** content pack from the **Unreal Engine Marketplace** as some of the content from the collection will be used in the following Quick Start. Once the Open World Demo Collection is downloaded add it to the project that you are using to follow along with this Quick Start by doing the following.

1. From the Epic Games Launcher in the Marketplace locate and then download the **Open World Demo Collection**.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63748538-cc4d-46e6-bf6e-abf6322139c2/04-t-owt-owdc.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63748538-cc4d-46e6-bf6e-abf6322139c2/04-t-owt-owdc.png)

   Click image for full size.

1. Go the **Library** section of the launcher and then under **Vault** section locate the Open World Demo Collection .

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c9c4f09-910e-45c1-b383-6e301fedf56f/05-t-owt-add-content-00.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c9c4f09-910e-45c1-b383-6e301fedf56f/05-t-owt-add-content-00.png)

   Click image for full size.

1. Click on the button that says **Add to Project**.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8fcc82cf-170c-4b0e-a317-13b91cc99a15/06-t-owt-add-to-project.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8fcc82cf-170c-4b0e-a317-13b91cc99a15/06-t-owt-add-to-project.png)

   Click image for full size.

1. You will then be shown a list of projects that you can add this to, select the project that you are using to follow along with this Quick Start and then press the **Add to Project** button

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/71857739-5123-4718-a680-fdaf0bdfe944/07-t-owt-atp.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/71857739-5123-4718-a680-fdaf0bdfe944/07-t-owt-atp.png)

   Click image for full size.

## 1 - Creating Foliage Type Actors

In this step you will create a new Level, Landscape Terrain, and all of the Assets the Procedural Foliage Tool requires.

1. Create a new level using the **Default Template** as a base.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7340440a-3695-4f72-991c-2515e55ef12b/08-t-new-level.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7340440a-3695-4f72-991c-2515e55ef12b/08-t-new-level.png)

   Click image for full size.

1. Add a new **Landscape Actor** to the level by first selecting **Landscape** in the **Modes** dropdown menu to open the **Landscape Panel**, and then clicking the **Create** button to add the Landscape Actor to the level.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b8a357b-cdc7-43ff-a3f4-92da940e1492/09-modes-landscape.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b8a357b-cdc7-43ff-a3f4-92da940e1492/09-modes-landscape.png)

   Click image for full size.

   

   Using a Landscape Terrain Actor quickly provides you with a very large area to spawn your forest on.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/51ee9966-fed1-4062-85dd-648224b7583c/10-placed-landscape.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/51ee9966-fed1-4062-85dd-648224b7583c/10-placed-landscape.png)

   Click image for full size.

   

   If you are not familiar with how Landscape Terrain works or would like to learn more, please refer to [Landscape Outdoor Terrain](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-outdoor-terrain-in-unreal-engine) for more information.

1. Create a new Procedural Foliage Spawner by **right-clicking** in the **Content Browser**, expanding the **Foliage** section, and then clicking on the **Procedural Foliage Spawner**.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c602a333-facc-488b-a777-ec501616056f/11-t-create-pfs.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c602a333-facc-488b-a777-ec501616056f/11-t-create-pfs.png)

   Click image for full size.

1. Name the Procedural Foliage Spawner in this example **PFS_Example** or something similar.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca3e6eff-b14e-4611-82ee-0b86ac0c63b3/12-t-name-pfs.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca3e6eff-b14e-4611-82ee-0b86ac0c63b3/12-t-name-pfs.png)

   Click image for full size.

1. Drag the Procedural Foliage Spawner from the **Content Browser** into the level and position it so that it is in the center of the level or at **0,0,200** in the X, Y, and Z axis.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0325b9f-2191-4773-a9d0-c52cab792246/13-pfs-place-pfs.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0325b9f-2191-4773-a9d0-c52cab792246/13-pfs-place-pfs.png)

   Click image for full size.

1. Scale the Procedural Foliage Spawner to **100,100,10** in the X, Y, and Z axis to create a large area to spawn your forest in.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9eea433-b4a0-47f5-98b6-e7aa0362df0e/14-pfs-example-details.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9eea433-b4a0-47f5-98b6-e7aa0362df0e/14-pfs-example-details.png)

   Click image for full size.

1. Now that we have our spawner, we need to give it some Foliage to spawn. To do this, **right - click** in the **Content Browser** expanding the **Foliage** section and then click on **Static Mesh Foliage**. Name the Static Mesh Foliage **Tree_00** or something similar.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/469bfd7d-b770-4556-8402-b32eaca864fa/15-t-create-ft.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/469bfd7d-b770-4556-8402-b32eaca864fa/15-t-create-ft.png)

   Click image for full size.

1. If you have not done so already, save your work and level by pressing the **Save All** button to save all content and the **Save** button to save the level. When prompted for a level name use the name **PFT_00**. At this point you should have something that looks similar to the image below.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d9f512a-ebb5-4a16-982e-7fc539a4ab5f/16-t-save-all.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d9f512a-ebb5-4a16-982e-7fc539a4ab5f/16-t-save-all.png)

   Click image for full size.

## 2 - Telling the Spawner What to Spawn

In the following section we will cover how to set up the **Foliage Type Actors** to work with the Procedural Foliage Spawner. You will continue to work with the **PFT_00** level that was created in the last step.

1. Open up the **Procedural Foliage Spawner** by **double - clicking** in the Content Browser.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e843696-5b57-4478-b85c-27a5b65a164f/17-t-pfs-opened.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e843696-5b57-4478-b85c-27a5b65a164f/17-t-pfs-opened.png)

   Click image for full size.

1. Add a new item to the **Foliage Types** array by clicking the **Plus Sign** icon that is to the right of the **Foliage Types** menu option.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc5821cf-223f-449c-81cc-ce38dddc352c/18-t-pfs-add-ft.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc5821cf-223f-449c-81cc-ce38dddc352c/18-t-pfs-add-ft.png)

   Click image for full size.

1. In the Content Browser, select the Tree_00 Static Mesh Foliage and drag it into the **Foliage Type Object**, or press the **Arrow** icon, to load the selected Static Mesh Foliage into the Procedural Foliage Spawner.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e329c39-5457-4f1a-a4de-eb97f26952d7/19-pfs-add-foliage-mesh.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e329c39-5457-4f1a-a4de-eb97f26952d7/19-pfs-add-foliage-mesh.png)

   Click image for full size.

1. Open up the Tree_00 Static Mesh Foliage by **double - clicking** on it in the Content Browser.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f08189dd-d667-46fe-80f0-76fd5c78d1bc/20-t-pft-window.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f08189dd-d667-46fe-80f0-76fd5c78d1bc/20-t-pft-window.png)

   Click image for full size.

1. At the top of the Tree_00 Static Mesh Foliage, locate the **Mesh** section and then click on the drop down menu that says **None**.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e4d2fc4-ab1d-423a-844f-2bad92e0b007/21-t-pft-mesh-section.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e4d2fc4-ab1d-423a-844f-2bad92e0b007/21-t-pft-mesh-section.png)

   Click image for full size.

1. Locate the **HillTree_02** Static Mesh from the **Open World Demo Collection** either by typing "HillTree_02" as the search term or by scrolling through the list, and load it by clicking on it.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66cf35b4-1b5c-4f70-a57f-2371f1a0645c/22-pfs-select-hill-tree-02.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66cf35b4-1b5c-4f70-a57f-2371f1a0645c/22-pfs-select-hill-tree-02.png)

   Click image for full size.

1. Back in the viewport select the **Procedural Foliage Spawner** that was placed in the level and then expand the **Procedural Foliage** section under the **Details** panel.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b917222-3fb4-4a5b-b7c8-6dab26dec6f0/23-t-pfv-select-in-level.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b917222-3fb4-4a5b-b7c8-6dab26dec6f0/23-t-pfv-select-in-level.png)

   Click image for full size.

1. Under the **Procedural Foliage** section click on the **Resimulate** button and you should now see the Procedural Foliage Spawner densely packed with tress like in the image below.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5491a7a6-26bf-463a-9aac-962a98123f46/24-t-final-results.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5491a7a6-26bf-463a-9aac-962a98123f46/24-t-final-results.png)

   Click image for full size.

   

   In order to see the proper results, you will need to click on **Build** in the **Main Toolbar** to rebuild the lighting every time you use the Resimulate button to create or alter the Procedural Foliage . This can take a long time due to the large number of static meshes involved.

## 3 - Tweaking Foliage Type Object Properties

**Foliage Type Objects** (both Static Mesh Foliage and Actor Foliage) come with a number of different properties that you can adjust to control anything from how the Foliage Type Objects are placed on other objects in the level to how the Foliage Type Objects will grow and spread throughout the Foliage Spawner. In the following section we will take a look at what properties are available in **Foliage Type Objects** and how you can manipulate these properties to get the results you desire. You will continue to work with the **PFT_00** level that was used in the last step.

1. Open up the Tree_00 Static Mesh Foliage.

1. Expand the **Placement** section and make sure that both **Align to Normal** and **Random Yaw** are enabled.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8b704de-ef6a-4e31-91c0-158f13b5000b/25-t-placement-options.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8b704de-ef6a-4e31-91c0-158f13b5000b/25-t-placement-options.png)

   Click image for full size.

   

   The Placement section is where you can adjust how a Foliage Type Object's meshes are placed on objects in the level.

1. Under the **Procedural** section of the Static Mesh Foliage expand the **Collision** section and set the **Shade Radius** to **50**.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e1c9d56-d26c-4bfa-969c-d32e0f1882a0/26-t-shade-radius.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e1c9d56-d26c-4bfa-969c-d32e0f1882a0/26-t-shade-radius.png)

   Click image for full size.

   

   The Collision section determines which Foliage Type Objects should be removed when two Foliage Type Objects are competing for the same spawn location or relative space. When a Virtual Seed's collision radius overlaps an existing collision or shade radius from another Foliage Type Object's Virtual Seed, one Virtual Seed will be replaced or killed based on which Foliage Type Object has the higher priority.

1. Select the Procedural Foliage Spawner that was placed in the level and under the Procedural Foliage section click on the Resimulate button.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc525e6e-3258-447b-aef3-23d5e99b92a1/27-t-press-resimulate.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc525e6e-3258-447b-aef3-23d5e99b92a1/27-t-press-resimulate.png)

   Click image for full size.

1. Back in the Tree_00 Static Mesh Foliage collapse the Collision section and expand the **Clustering** section, then set **Num Steps** to **0**, so that we get trees that are all the same size and age and then press the Resimulate button. When completed you should have something that looks similar to the image below.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5673039b-6662-4aa6-b8f8-df8a124e5a6f/28-t-num-steps-0.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5673039b-6662-4aa6-b8f8-df8a124e5a6f/28-t-num-steps-0.png)

   Click image for full size.

   

   Clustering uses a number of properties such as density, age, and proximity to help determine how the specified Foliage Type Object's mesh instances should be placed, grouped and spread around inside of the Procedural Foliage Spawner.

1. While we now have some space in between our trees, the overall density is still a little too high. To fix this, set the **Initial Seed Density** to **0.25** and then click on the Resimulate button.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1959eac-e46b-4fb4-af79-ae7cf1647417/29-t-num-isd-0-125.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1959eac-e46b-4fb4-af79-ae7cf1647417/29-t-num-isd-0-125.png)

   Click image for full size.

1. As you can see, setting the Initial Seed Density to 0.25 greatly reduced the density of our forest because we are only growing and spreading trees for a single year. To fix this set the Num Steps back to **3**, which will grow and spread the trees for 3 years, and then click on the Resimulate button.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1ce2863-5cc5-4cf5-b4ff-c35614623c8c/30-t-num-steps-3.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1ce2863-5cc5-4cf5-b4ff-c35614623c8c/30-t-num-steps-3.png)

   Click image for full size.

1. Expand the **Growth** section then set the following parameters to the following settings.

   - **Max Age**: **20.0**
   - **Procedural Scale Max**: **10.0**

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fccfe258-e6cd-4d4e-bf9b-a7854e2b6b43/31-t-set-growth.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fccfe258-e6cd-4d4e-bf9b-a7854e2b6b43/31-t-set-growth.png)

   Click image for full size.

   

   The Growth section allows you to adjust how a Foliage Type Object's mesh instances will grow and get bigger over time.

1. Finally in the **Instance Settings** under the **Cull Distance** option, set the **Max** value to **20,000** and then click on the Resimulate button. When completed you should have something that looks similar to the image below.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9495e39-3319-4afc-9480-d2274543cccc/32-t-cull-distance.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9495e39-3319-4afc-9480-d2274543cccc/32-t-cull-distance.png)

   Click image for full size.

   

   The Instance Settings allows you to adjust how a Foliage Type Object's mesh instances will be displayed in the level. Inside the Instance Settings you can set or adjust many different properties like Cull Distance, Shadowing, and Collision.

## 4 - Using Multiple Foliage Type Objects

Adding another species of tree to your virtual forest will greatly help to increase the realism and overall look and feel. Luckily, the **Procedural Foliage Spawner** allows for you to spawn multiple **Foliage Type Objects** resulting in one single **Procedural Foliage Spawner** being able to spawn an entire forest with a multitude of different trees. In the following section we will take a look at how you can set up a Procedural Foliage Spawner to work with multiple Foliage Types. You will be continuing to work with the **PFT_00** level that was used in the last step.

1. Inside of the Content Browser select the Tree_00 Static Mesh Foliage and then press **Ctrl + W** on the keyboard to duplicate it using **Tree_01** as the name.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e36415c0-da87-4df0-841e-b3b003099dce/33-t-dup-ft.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e36415c0-da87-4df0-841e-b3b003099dce/33-t-dup-ft.png)

   Click image for full size.

1. Open the newly created Tree_01 Static Mesh Foliage and under the Mesh section change the mesh to the **ScotsPineTall_01** Static Mesh.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d36f2d1-7974-45a6-b5cd-ed2dcf8a8fbd/34-t-new-mesh.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d36f2d1-7974-45a6-b5cd-ed2dcf8a8fbd/34-t-new-mesh.png)

   Click image for full size.

1. Open up the Procedural Foliage Spawner from the Content Browser and expand the Foliage Types section.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67d14d6c-6cca-4bcb-8cc7-d71c9c13fbfb/35-t-expand-ft.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67d14d6c-6cca-4bcb-8cc7-d71c9c13fbfb/35-t-expand-ft.png)

   Click image for full size.

1. Click on the Plus sign icon to add the option to input another Foliage Type Object.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16f8b408-20f2-40c7-b7e0-eeef8d3607dc/36-t-add-new-ft.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16f8b408-20f2-40c7-b7e0-eeef8d3607dc/36-t-add-new-ft.png)

   Click image for full size.

1. In the Content Browser, select the Tree_01 Static Mesh Foliage and drag it into the Foliage Type Object, or press the Arrow icon, to load the selected Static Mesh Foliage into the Procedural Foliage Spawner.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/45935b54-4e64-4533-a07f-5134d43db181/37-pfs-add-foliage-mesh-2.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/45935b54-4e64-4533-a07f-5134d43db181/37-pfs-add-foliage-mesh-2.png)

   Click image for full size.

1. Select the Procedural Foliage Spawner that was placed in the level and then click on the Resimulate button. When completed you should see something like the following image.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f0f49a5-a156-4272-9111-d5eff9b37732/38-t-2-ft-in-level.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f0f49a5-a156-4272-9111-d5eff9b37732/38-t-2-ft-in-level.png)

   Click image for full size.

1. To make the forest look more interesting open up the Tree_01 Static Mesh Foliage and adjust the following parameters with the following values. The numbers and options that are listed below were selected because they will produce a forest that has interesting clustering and growth interaction with the Static Mesh Foliage instances that are already in use. However please feel free to experiment with these numbers and settings till you get something that suits your needs.

   - **Num Steps:** 4
   - **Initial Seed Density:** 0.125
   - **Average Spread Distance:** 100
   - **Can Grow in Shade:** Enabled
   - **Spawns in Shade:** Enabled
   - **Max Age:** 15
   - **Overlap Priority:** 1
   - **Procedural Scale:** Max 5.0

1. Once the settings have been adjusted click on the **Resimulate** button on the Procedural Foliage Spawner and you should now have something that looks similar to the image below.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/820c59db-8352-42d5-82f8-9bb654b94845/39-t-ft01-adjust-settings.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/820c59db-8352-42d5-82f8-9bb654b94845/39-t-ft01-adjust-settings.png)

   Click image for full view.

## 5 - Implementing Procedural Foliage Blocking Volumes

The **Procedural Foliage Blocking Volume** is a Volume Actor that can be placed in a level and scaled to a desired size which will prevent the Procedural Foliage Spawner from spawning any Foliage Type Objects inside of the bounds of the Procedural Foliage Blocking Volume. In the following section we will go over how you can add a **Procedural Foliage Blocking Volume** to your level and use it to prevent Foliage meshes from spawning. You will be continuing to work with the **PFT_00** level that was used in the last step.

1. First find the **Procedural Foliage Blocking Volume** by searching for it in the **Place Actors** panel using **Proc** as the search term.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b2f6bb3-1605-42fa-b469-034a8f04f7c7/40-t-find-procf-blocking-volume.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b2f6bb3-1605-42fa-b469-034a8f04f7c7/40-t-find-procf-blocking-volume.png)

   Click image for full size.

1. Select the Procedural Foliage Blocking Volume and then drag it from the Place Actors panel into the level.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e5466eee-e2dd-4895-bb67-50a4f7bfd138/41-pfs-blocking-volume.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e5466eee-e2dd-4895-bb67-50a4f7bfd138/41-pfs-blocking-volume.png)

   Click image for full size.

1. To stop foliage meshes from being spawned in the back portion of the Procedural Foliage Spawner move and scale the Procedural Foliage Blocking Volume using the following location and scale values.

   - **Location X:** 5430.0 cm
   - **Location Y:** -3900.0 cm
   - **Location Z:** 200.0 cm
   - **Scale X:** 41.75
   - **Scale Y:** 65.5
   - **Scale X:** 41.75

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0baefe5-a87e-478b-9509-201f89134b7b/42-t-pfbv-postion.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0baefe5-a87e-478b-9509-201f89134b7b/42-t-pfbv-postion.png)

   Click image for full size.

1. Now select the Procedural Foliage Spawner in the level and then in the Details click on the Resimulate button. When the Resimulate is completed you should now be missing the entire back section of trees that were intersecting with the Procedural Foliage Blocking Volume.

   [![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2d64b16-5ec2-408f-b6a2-3e272dd1822f/43-t-pfv-before-after.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2d64b16-5ec2-408f-b6a2-3e272dd1822f/43-t-pfv-before-after.png)

   Click image for full size.

   In the following image we can see the before and after results.

   | Image Number | Results                                            |
   | ------------ | -------------------------------------------------- |
   | 1:           | Before Procedural Foliage Blocking Volume is added |
   | 2:           | After Procedural Foliage Blocking Volume is added  |

## 6 - On Your Own!

Now that you have seen that power the Procedural Foliage tool offers, try using the tools listed below in conjunction with what you just learned about the Procedural Foliage tool to try and make a level that looks like the following image.

![On Your Own](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f5dffba-150c-4398-9640-878f567ebf20/44-t-on-your-own.png)

- Try using Foliage Actors instead of Static Mesh Foliage.
- Use the [Grass Tool](https://dev.epicgames.com/documentation/en-us/unreal-engine/grass-quick-start-in-unreal-engine) to make the Landscape look like it is densely covered in grass, flowers and bushes.
- Define the look and feel of the Landscape terrain using the [Landscape Sculpt](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-sculpt-mode-in-unreal-engine) tools add things like hills, mountains and lakes.
- Give the surface of the Landscape more visual variety and detail by creating a [Landscape Material](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-materials-in-unreal-engine) that has multiple Textures that can be painted on the Landscape terrain.
- Adjust the [Directional Light](https://dev.epicgames.com/documentation/en-us/unreal-engine/directional-lights-in-unreal-engine) to make the level lighting resemble lighting that happens in the early morning or late afternoon.
- Set up the level lighting to use a completely dynamic based lighting solution that will make use of dynamic shadows as well as [Ray Traced Distance Field Soft Shadows](https://dev.epicgames.com/documentation/en-us/unreal-engine/distance-field-soft-shadows-in-unreal-engine).
- Try using the [Foliage System](https://dev.epicgames.com/documentation/en-us/unreal-engine/foliage-mode-in-unreal-engine) tools to remove or tweak the placement, rotation and scale of the Foliage meshes that are placed by the Procedural Foliage tool so that you can get the exact look you are going for.
- Show off your creation to others by using a [Camera](https://dev.epicgames.com/documentation/en-us/unreal-engine/camera-actors-in-unreal-engine) in conjunction with [Sequencer](https://dev.epicgames.com/documentation/en-us/unreal-engine/real-time-compositing-with-sequencer-in-unreal-engine) to render out a video of your level for you to share with the world.