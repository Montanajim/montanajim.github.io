# World vs Local



In Unreal Engine, the terms "world" and "local" refer to different coordinate systems used to describe the position, rotation, and scale of objects.

**World Coordinate System:**

- This system is based on a fixed, global reference point in the world.
- It is used to describe the position of an object relative to the entire world.
- Changes to the world coordinate system affect the positions of all objects in the world.

**Local Coordinate System:**

- This system is based on the origin and axes of an individual object.
- It is used to describe the position, rotation, and scale of an object relative to its own origin.
- Changes to the local coordinate system only affect the object itself.

**Key Differences:**

- **Reference point:** World coordinates use a global reference point, while local coordinates use the object's origin.
- **Scope:** Changes to world coordinates affect all objects, while changes to local coordinates only affect the specific object.
- **Relative or absolute:** World coordinates are absolute, while local coordinates are relative to the object's origin.

**Example:**

- If you want to move an object 100 units forward, you can use the `Add Actor World Offset` node to add 100 units to its Z-axis in the world coordinate system.
- If you want to move the object 100 units forward relative to its own orientation, you can use the `Add Actor Local Offset` node to add 100 units to its Z-axis in the local coordinate system.

**Understanding the difference between world and local coordinates is crucial for accurate object manipulation and positioning in Unreal Engine.**





---

In Unreal Engine, "world" refers to the global coordinate system, where all objects are positioned relative to the entire level, while "local" refers to the coordinate system specific to an individual object, meaning its position and rotation are defined relative to its own center point, regardless of its position in the world; 

essentially, "local" is like looking at the object from its own perspective.

Key points about world and local:

- World space:
  - Represents the overall level layout.
  - If you move an object in world space, it moves relative to the entire level, not just its parent.
  - Useful for positioning objects within the game world.
- Local space:
  - Represents the object's own coordinate system.
  - If you rotate an object in local space, it rotates based on its own axis, not the world's axis.
  - Useful for manipulating an object's relative position or rotation within itself.

Example:

- Imagine a car in a game:

  - Moving the car "forward" in world space would move it straight ahead in the level.

  - Rotating the car "right" in local space would turn its steering wheel to the right, even if it's already moving.

    

     