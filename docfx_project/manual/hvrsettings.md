# HVRSettings

Stores framework wide settings and access via a singleton. 

Auto-generated under HurricaneVR/Framework/Resources.

Can be moved to any 'Resources' folder outside of the asset if modified to prevent loss if deleting the asset folder to update (not usually required but sometimes I need to re-org files).

Holds local directory references which are populated when generated, if you move the asset folder then these references need to manually updated.

## Auto Apply Grabbable Layer

Globally enable / disable the application of the "Grabbable" layer to grabbable objects on start.

## Default Socketable Tags

Newly added [HVRTagSocketFilter](xref:HurricaneVR.Framework.Core.Sockets.HVRTagSocketFilter) and [HVRTagSocketable](xref:HurricaneVR.Framework.Core.Sockets.HVRTagSocketable) components will populate their Tags field if this is populated to help ease the work flow.

Read about [Scriptable Object Based Filtering](sockets.md#scriptable-object-based-filtering).

# Pose Settings

- Left / Right Hand: Prefabs used by the HVRHandPoser to save grab point poses.
- Inverse Kinematics: lets the HVRHandPoser know to use the individual hand prefabs or the Full Body prefab.
- HandPoseHandleOffset: when the hand poser prefabs are active, this offset is applied to the gizmo in the scene editor to prevent overlap with the transform gizmos.
- Open Hand Pose: new poses created in the HVRHandPoser will use this as the base pose, otherwise the hand prefab will be used as it's set.
- Poser Shows One Finger: when posing hands each bone has a gizmo, enable this if you only want one finger's bone gizmos to be visible at a time. Selecting the root bone of another finger will switch fingers.

# Hand Poser Finger Curl Defaults

The HVRHandPoser makes use of the finger tracking and capacitive button finger curl values supplied by the controllers. Their values are managed by the [Finger Settings](scenesetup.md#finger-settings) scriptable object.

When a new pose is added with a HVRHandPoser, the finger curl settings will be pulled from these values to save time setting up poses if you want finger tracking to affect your hand poses when holding objects (like boneworks).

# Grab Detection

Explained in the [Grabbable Detection](detection.md#grabbable-detection) page.

# Joint Setting Defaults

- Default Joint Settings: the default [HVRJointSettings](jointsettings.md#hvrjointsettings) applied to the [Configurable Joint](https://docs.unity3d.com/Manual/class-ConfigurableJoint.html) between the hand and the held object.

- Line Grab Settings: the [HVRJointSettings](jointsettings.md#hvrjointsettings) applied to the [Configurable Joint](https://docs.unity3d.com/Manual/class-ConfigurableJoint.html) between the hand and the held object when the grab point is a line grab.

# Debugging

- Verbose Grabbable Events: Grabbable spits out log statements during it's grab sequences.
- Verbose Hand Grabber Events: Hand grabber spits out log statements during it's grab sequences.
- Disable Haptics (v2.8.2+): Completely disables the call to the device haptic functions to save on battery life during testing.
