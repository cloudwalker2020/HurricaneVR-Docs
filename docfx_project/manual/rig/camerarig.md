# [HVRCameraRig](xref:HurricaneVR.Framework.Core.Player.HVRCameraRig)

The camera rig component manages offsetting the HMD / Camera. 

Height calibration is included and can be enabled by setting the [SitStanding](xref:HurricaneVR.Framework.Core.Player.HVRCameraRig.SitStanding) along with the [EyeHeight](xref:HurricaneVR.Framework.Core.Player.HVRCameraRig.EyeHeight) field.

To assist with testing in edit mode, I have added logic that can quickly calibrate height after entering play mode.
- [SaveCalibrationHeight](xref:HurricaneVR.Framework.Core.Player.HVRCameraRig.SaveCalibrationHeight): if enabled the last calibrated height is stored in player prefs.
- Enabling [DebugCalibMode](xref:HurricaneVR.Framework.Core.Player.HVRCameraRig.DebugCalibMode) will force height calibration on start, if [SaveCalibrationHeight](xref:HurricaneVR.Framework.Core.Player.HVRCameraRig.SaveCalibrationHeight) is enabled it's stored value is used, otherwise the HMD height is used.
    - HMDMoved: Calibrates when the HMD moves more than [DebugCalibMovedThreshold](xref:HurricaneVR.Framework.Core.Player.HVRCameraRig.DebugCalibMovedThreshold) from it's starting position.
    - Immediately: Immediately calibrates.
- [DebugKeyboardRecalibrate](xref:HurricaneVR.Framework.Core.Player.HVRCameraRig.DebugKeyboardRecalibrate) is enabled and RecalibrateKey pressed.

## FloorOffset

This transform moves up and down based on a few variables.
- Height Calibration: Calibrating in sitting mode will offset based on the difference between device height and [EyeHeight](xref:HurricaneVR.Framework.Core.Player.HVRCameraRig.EyeHeight).
- [PlayerControllerYOffset](xref:HurricaneVR.Framework.Core.Player.HVRCameraRig.PlayerControllerYOffset): Used by the player controller when a input driven crouch is activated.
- [CameraYOffset](xref:HurricaneVR.Framework.Core.Player.HVRCameraRig.CameraYOffset): Users can adjust this on demand to raise or lower the camera. If [DebugKeyboardOffset](xref:HurricaneVR.Framework.Core.Player.HVRCameraRig.DebugKeyboardOffset) is enabled the Up/Down arrow keys will shift by [DebugKeyboardIncrement](xref:HurricaneVR.Framework.Core.Player.HVRCameraRig.DebugKeyboardIncrement) amount.


## Camera Scale

When the [SitStanding](xref:HurricaneVR.Framework.Core.Player.HVRCameraRig.SitStanding) mode is set to Standing, this transform will scale based on the device reported Y height and the [EyeHeight](xref:HurricaneVR.Framework.Core.Player.HVRCameraRig.EyeHeight) field.

This will make the world look smaller for shorter players, and larger for taller players if their height is not close to the [EyeHeight](xref:HurricaneVR.Framework.Core.Player.HVRCameraRig.EyeHeight) value.

Using this feature will let you build your world without worrying about how tall the player is. You can see this in action in games like Boneworks and Blade and Sorcery.

## Left / Right Controller

Transforms that represent the tracked controller device positions and rotations.

Each transform has an Offset transform child used to shift the physics hand target.

The [HVRControllerOffset](xref:HurricaneVR.Framework.Components.HVRControllerOffset) component on the Offset transform manages the position and rotation offset based on the Unity XR plugin and device connected. The offsets are driven by the [Controller Offsets](../scenesetup.md#controller-offsets) field on the [HVRInputManager](xref:HurricaneVR.Framework.ControllerInput.HVRInputManager) component.