# Unreal Editor Interface



Overview of the key elements of the Unreal Editor interface

![Unreal Editor Interface](https://dev.epicgames.com/community/api/documentation/image/fd12eabd-75cc-40f9-8149-1f8249e3d094?resizing_type=fit&width=1920)

This page describes the most common elements of the **Unreal Engine 5 interface** and what they do. It also links to other pages where you can learn more. Some of the elements described on this page, such as panels and menu bars, are generally the same across various parts of the engine. You should spend some time getting familiar with their general purpose and and functionality, especially if you're new to developing games and applications with Unreal Engine.

When you open Unreal Engine 5 for the first time, the **Level Editor** opens. You will see the following window:

[![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0fab641-4dee-4ef3-821a-0a022d37bf5a/ue5-default-interface.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0fab641-4dee-4ef3-821a-0a022d37bf5a/ue5-default-interface.png)

Default Unreal Editor interface in Unreal Engine 5. Click the image for full size.

| **Number** | **Name**                  | **Description**                                              |
| ---------- | ------------------------- | ------------------------------------------------------------ |
| 1          | **Menu Bar**              | Use these menus to access editor-specific commands and functionality. |
| 2          | **Main Toolbar**          | Contains shortcuts for some of the most common tools and editors in Unreal Engine, as well as shortcuts to enter **Play** mode (run your game inside Unreal Editor) and to deploy your project to other platforms. |
| 3          | **Level Viewport**        | Displays the contents of your Level, such as Cameras, Actors, Static Meshes, and so on. |
| 4          | **Content Drawer** button | Opens the **Content Drawer**, from which you can access all of the Assets in your Project. |
| 5          | **Bottom Toolbar**        | Contains shortcuts to the Command Console, Output Log, and Derived Data functionality. Also displays source control status. |
| 6          | **Outliner**              | Displays a hierarchical tree view of all content in your Level. |
| 7          | **Details** panel         | Appears when you select an Actor. Displays various properties for that Actor, such as its **Transform** (position in the Level), Static Mesh, Material, and physics settings. This panel displays different settings depending on what you select in the Level Viewport. |

## Menu Bar

![A menu bar in Unreal Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/360dc3bc-659d-483b-98e1-b86a9bb09b31/menu-bar.png)

Each editor in Unreal Engine has a **menu bar** that is located in the top-right of that editor window (Windows) or at the top of the screen (macOS). Some of the menus, such as **File**, **Window**, and **Help**, are present in all editor windows, not just the Level Editor. Others are editor-specific.

## Main Toolbar

The **Main Toolbar** contains shortcuts to some of the most used tools and commands in Unreal Editor. It is divided into the following areas:

![The Main Toolbar in Unreal Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f00bcf82-b2b1-41d0-9cfe-0b873e0ab94a/main-toolbar.png)

### 1. Save Button

Click this button to save the Level that is currently open.

### 2. Mode Selection

Contains shortcuts for quickly switching between different modes to edit content within your Level:

- Select Editing
- Landscape Editing
- Foliage Editing
- Mesh Painting
- Fracture Editing
- Brush Editing

### 3. Content Shortcuts

Contains shortcuts for adding and opening common types of content within the Level Editor.

| **Shortcut**   | **Description**                                              |
| -------------- | ------------------------------------------------------------ |
| **Create**     | Choose from a list of common Assets to quickly add to your Level. You can also access the **Place Actors** panels from this menu. |
| **Blueprints** | Create and access Blueprints.                                |
| **Cinematics** | Create a Level Sequence or Master Sequence cinematic.        |

### 4. Play Mode Controls

Contains shortcut buttons (Play, Skip, Stop, and Eject) for running your game in the Editor.

### 5. Platforms Menu

Contains a series of options you can use to configure, prepare, and deploy your project to different platforms, such as desktop, mobile, or consoles.

### 6. Settings

Contains various settings for the Unreal Editor, Level Editor Viewport, and game behavior.

## Level Viewport

The **Level Viewport** displays the contents of the Level that is currently open. When you open a project in Unreal Engine, the project's default Level opens in the Level Viewport by default. This is where you can view and edit the contents of your active Level, whether it's a game environment, a product visualization app, or something else.

The Level Viewport can generally display the contents of the Level in two different ways:

- **Perspective**, which is a 3D view you can navigate to see the contents of the viewport from different angles.
- **Ortographic**, which is a 2D view that looks down one of the main axes (X, Y, or Z).

[![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19b3b84e-aff1-4d1e-a010-196f627df16c/viewport-examples.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19b3b84e-aff1-4d1e-a010-196f627df16c/viewport-examples.png)

Different views of the Level Viewport in Unreal Engine 5. Top: Perspective view. Bottom: Top-down ortographic view. Click the image for full size.

To learn more about the Level Viewport, refer to the pages below.

## Content Drawer and Content Browser

The **Content Browser** is a file explorer window that displays all of the Assets, Blueprints, and other files contained in your project. You can use it to browse through your content, drag Assets into the Level, migrate Assets between projects, and more.

[![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab5a2104-2b65-4906-952c-17810d7dd490/ue5_1-content-browser.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab5a2104-2b65-4906-952c-17810d7dd490/ue5_1-content-browser.png)

Content Browser window in Unreal Engine 5. Click the image for full size.

The **Content Drawer** button, located in the bottom-left corner of the Unreal Editor, opens a special instance of the Content Browser that automatically minimizes when it loses focus (that is, when you click away from it). To keep it open, click the **Dock in Layout** button in the top-right corner of the Content Drawer. This creates a new instance of the Content Browser, but you can still open a new Content Drawer.

## Bottom Toolbar

The Bottom Toolbar contains shortcuts to the Command Console, Output Log, and Derived Data functionality. It also displays source control status. It is divided into the following areas:

![The Bottom Toolbar in Unreal Engine 5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da2a3f9f-ae48-4fb1-8c50-43a9bd29b04a/bottom-toolbar.png)

| **Number** | **Name**                  | **Description**                                              |
| ---------- | ------------------------- | ------------------------------------------------------------ |
| 1          | **Output Log**            | Debugging tool that prints out useful information while your application is running. |
| 2          | **Command Console**       | Behaves as any other command line interface: enter console commands to trigger specific editor behaviors.Type `help` and press **Enter** to open a list of available console commands in your browser. |
| 3          | **Derived Data**          | Provides [Derived Data](https://dev.epicgames.com/documentation/en-us/unreal-engine/derived-data-settings-in-the-unreal-engine-project-settings) functionality. |
| 4          | **Source Control Status** | Displays source control status if your project is connected to source control (for example, GitHub or Perforce). Otherwise, this will say *Source Control Off*. |

## Outliner

The **Outliner** panel (formerly known as World Outliner) displays a hierarchical view of all content in your Level. By default, it is located in the upper-right corner of the Unreal Editor window. You can have up to four different Outliners, each with its own column layout and filter configuration.

![Outliner panel in Unreal Engine 5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a45e9195-7ec5-406b-a379-9965721445b3/ue5_1-outliner.png)

You can also use the Outliner panel to:

- Quickly hide or reveal Actors by clicking their associated **Eye** button.
- Access an Actor's **context menu** by right-clicking that Actor. You can then perform additional, Actor-specific operations from that menu.
- Create, move, and delete content folders.

## Details Panel

When you select an Actor in the Level Viewport, the **Details** panel will show the settings and properties that affect the Actor you selected. By default, it is located on the right side of the Unreal Editor window, under the **World Outliner** panel.

[![img](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3589f1d7-6e41-4ba0-9bd9-ec26b548d4f2/details-panel.png)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3589f1d7-6e41-4ba0-9bd9-ec26b548d4f2/details-panel.png)

This example shows a cube Static Mesh Actor's Details panel. With the cube Static Mesh selected, the Details Panel appears docked to the right-hand side of the Unreal Editor. Click the image for full size.