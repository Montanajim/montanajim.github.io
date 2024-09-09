

## Blueprint Commands to Manipulate Objects in Unreal Engine

**Blueprint nodes** are the building blocks for creating interactive game elements in Unreal Engine. Here are some common nodes used to manipulate objects:

### Movement and Rotation

- **Set Actor Location:** Sets the absolute location of an actor.
- **Set Actor Rotation:** Sets the absolute rotation of an actor.
- **Add Actor World Offset:** Adds an offset to the actor's world location.
- **Add Actor Local Offset:** Adds an offset to the actor's local location.
- **Add Actor World Rotation:** Adds a rotation to the actor's world rotation.
- **Add Actor Local Rotation:** Adds a rotation to the actor's local rotation.
- **Rotate Actor Around Axis:** Rotates an actor around a specified axis.

### Scaling

- **Set Actor Scale3D:** Sets the scale of an actor along the X, Y, and Z axes.
- **Add Actor World Scale3D:** Adds a scale factor to the actor's world scale.
- **Add Actor Local Scale3D:** Adds a scale factor to the actor's local scale.

### Other Manipulations

- **Destroy Actor:** Destroys an actor.
- **Enable Actor:** Enables or disables an actor.
- **Set Actor Hidden in Game:** Hides or unhides an actor in the game.
- **Get Actor Bounds:** Gets the bounding box of an actor.
- **Get Actor Location:** Gets the absolute location of an actor.
- **Get Actor Rotation:** Gets the absolute rotation of an actor.
- **Get Actor Scale3D:** Gets the scale of an actor.

### Examples

**To move an actor forward 100 units:**

1. Get the actor's current location.
1. Add 100 units to the Z-axis of the location.
1. Set the actor's location to the new value.

**To rotate an actor 90 degrees around the Y-axis:**

1. Get the actor's current rotation.
1. Create a quaternion representing a 90-degree rotation around the Y-axis.
1. Add the rotation quaternion to the actor's current rotation.
1. Set the actor's rotation to the new value.

**Remember:** The specific nodes and their usage can vary depending on the context and the type of object you're manipulating. Experiment with different combinations to achieve the desired effects.

**Would you like to see a more detailed example or explore a specific use case?**