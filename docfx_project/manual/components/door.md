# Physics Door Setup

This tutorial will be using the included '**swinging_door**' prefab as a guide.

1. First we setup the door rigidbody. Hopefully your door has the model pivot point set correctly at the side of the door for "hinge rotation". If not place the door as a child of an empty game object and use the empty to set the pivot point. The dummy pivot object would become your rigidbody.
1. Add the Rigidbody, HVRPhysicsDoor and HVRRotationTracker components to the door.
    1. :::image type="content" source="../../images/door_components.PNG" alt-text="door":::
    1. HVRPhysicsDoor will set the mass and gravity setting of the rigidbody. I use a default of 10 mass as the additional mass helps prevent joint stretching.
    1. Set the axis of rotation in the door and tracker components. Example door has a up vector of Y for rotation.
    1. Door Options:
        1. **Start Locked**: the door and handles if referenced, will not be openable until the Unlock method is executed on the component.
            1. The example scene includes an example of this. **key_door_setup** prefab.
        1. **Door Closing Settings:**
            1. When the door handle is not held, the door will automatically shut all the way if it's angle is lower than the **'Close Angle'**
            1. **Close Over Time** - the automatic closing will occur over this amount of time.
            1. **Close Detection Time** the close sequence will start only if this amount of time has elapsed while the door angle is lower than **'Close Angle'**
        1. **SFX**
            1. Audio Clips can play when opened or closed based on the **SFX Threshold Angle** field.
            1. The timeout field delays playing the same clip again.
        1. **Joint Limits**
            1. Most doors will limit their rotation, enable Limit Rotation and set the desired min and max angle.
            1. Joint limit rotation will depend on the axis set. You can use the **Target Angular Velocity** setting to use torque to rotate the door in play mode to easily test your joint limits. (Requires non zero damper to work).
        1. **Joint Settings**
            1. Adjust the damper to add rotational difficulty (damper brings angular velocity to zero).
            1. Adjust the spring to control how fast the door will return to it's start rotation.

1. Next we setup the door handles. If you don't need rotating door handles skip this step. You can add two door handles in v2.8.6 and up.
    1. **Rigidbody** (I use mass of 10 for joint stability).
    1. **HVRPhysicsDial** - sets up the rotation joint with joint limits, spring, and damper.
        1. Set the axis of rotation.
        1. Set the 'Connected Body' to the door rigidbody.
        1. Assign the desired joint limits based on how far the handle will rotate.
        1. Joint Settings
            1. Grabbed Damper - rotation difficulty when held
            1. Damper - rotation difficulty when not held
            1. Spring - spring force to return to the starting rotation - 10:1 Spring:Damper ratio is a good starting point.
    1. **HVRRotationTracker** - will be used by the door component to detect handle rotation
        1. Set the axis of rotation
        1. Other settings can be ignored.
    1. **HVRGrabbable** - so we can grab the door handle
        1. [Grabbable Tutorial](https://youtu.be/HZQ6QdMmZ34)
        1. Disable force grabbing (unless you want to open the door handle in style :D)
        1. Enable Stationary so that the hand will move to the handle on grab.
    1. **HVRPhysicsDoor** - assign references
        1. Enable 'Handle Requires Rotation' and assign the references for one or both handles setup.
        1. Enablinge 'Hand Requires Rotation' causes the door to latch shut, and it will only unlatch if either handle is rotated beyond 'Handle Threshold' amount of degrees from it's start rotation.
1. Door Collision
    1. If you haven't already, you should add collision geometry to your door, frames, and handles.
    2. Take a look at the swinging_door prefab root. I use the HVRObjectCollisionDisabler component to make sure door parts don't collide with each other.
    3. Using this component will make all children colliders of the assigned transforms ignore collision with each other.
    4. :::image type="content" source="../../images/door_disable_collision.PNG" alt-text="ddc":::

Door Handle Components:

:::image type="content" source="../../images/door_handle_components.PNG" alt-text="dhc":::

Handle References on HVRPhysicsDoor:

:::image type="content" source="../../images/door_handle_refs.PNG" alt-text="refs":::
