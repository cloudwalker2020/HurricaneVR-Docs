# Scene Setup

## HVRGlobal

This prefab is used to hold framework required components and should be placed into a master scene in your game. It is advised to make a variant of this prefab so that you can override the fields of it's components to make updating the asset in the future painless.

## [HVRInputManager](xref:HurricaneVR.Framework.ControllerInput.HVRInputManager)

This component is required for the framework to function. It handles device detection and other various input functions. It automatically marks it's object as DontDestroyOnLoad so that it persists between scene changes.

The following fields are scriptable objects that you can clone to customize certain behaviours. Be sure to clone the original if you wish to modify the values and assign it in your own HVRGlobal prefab variant to make updating the asset easier for you.

### Finger Settings

[HVRFingerSettings](xref:HurricaneVR.Framework.Shared.HVRFingerSettings) scriptable object that defines how much each capacitive button affects the bending of each finger.

As of this writing, OpenXR via Unity still does not support Knuckles finger tracking out of the box, the  [KnucklesOverrideGripFingers](xref:HurricaneVR.Framework.Shared.HVRFingerSettings.KnucklesOverrideGripFingers)  can be enabled to fallback to standard finger curl behaviour like Oculus controllers.

### Controller Offsets

[HVRControllerOffsets](xref:HurricaneVR.Framework.Components.HVRControllerOffsets) scriptable object that defines controller offsets based on the active VR SDK and the device connected. 

### Grab Haptics
