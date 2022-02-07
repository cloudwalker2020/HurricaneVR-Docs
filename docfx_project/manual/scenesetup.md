# Scene Setup

The following provides a brief explanation of the required objects / components needed in your scene for the asset to function.

Example scene with the minimum required: /HurricaneVR/TechDemo/Scenes/scenes_barebones

HVRGlobal Prefab: /HurricaneVR/Framework/Prefabs
XR Rig Prefab: /HurricaneVR/TechDemo/Prefabs/ TechDemoXRRig | TechDemoXRRigOpenXR

# HVRGlobal

This prefab is used to hold framework required components and should be placed into a master scene in your game. It is advised to make a variant of this prefab so that you can override the fields of it's components so that updating the asset in the future painless.

## [HVRInputManager](xref:HurricaneVR.Framework.ControllerInput.HVRInputManager)

This component is required for the framework to function. It handles device detection and other various input functions. It automatically marks it's object as DontDestroyOnLoad so that it persists between scene changes.

The following fields are scriptable objects that you can clone to customize certain behaviours. Be sure to clone the original if you wish to modify the values and assign it in your own HVRGlobal prefab variant to make updating the asset easier for you.

## Finger Settings

[HVRFingerSettings](xref:HurricaneVR.Framework.Shared.HVRFingerSettings) scriptable object that defines how much each capacitive button affects the bending of each finger.

As of this writing, OpenXR via Unity still does not support Knuckles finger tracking out of the box, the  [KnucklesOverrideGripFingers](xref:HurricaneVR.Framework.Shared.HVRFingerSettings.KnucklesOverrideGripFingers)  can be enabled to fallback to standard finger curl behaviour like Oculus controllers.

## Controller Offsets

[HVRControllerOffsets](xref:HurricaneVR.Framework.Components.HVRControllerOffsets) scriptable object that defines controller offsets based on the active VR SDK and the device connected. 

## Grab Haptics

[HVRGrabHaptics](xref:HurricaneVR.Framework.Shared.HVRGrabHaptics) defines haptic values used in the following interaction events:
- Hand Grab
- Hand Release
- Hand Hover
- Force Grab
- Force Hover

## Deadzones

Not entirely sure how useful device specific deadzones is, but each device can have a deadzone value applied. 
'Override Deadzone' and 'Deadzone Override' can be used to provide a single deadzone value.

The controller component will ignore values less than the provided deadzones when reading thumbstick inputs.