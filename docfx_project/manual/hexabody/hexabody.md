# HexaBody

This player controller was modelled after the Boneworks player controller which uses:
1. A rolling ball for locomotion.
1. Height calibration for fixed height player.
1. Inverse forces applied to the player via the Hand rigidbodies
1. Crouching and Jumping which is driven by lifting the lower ball / knee up and down.

## Height Calibration

The player is required to calibrate their height as the HexaBody is fixed height. The 'Eye Height' field under the Body Adjustment section of HexaBodyPlayer4 component drives the height calibration.

The default 1.66m is chosen since the average male height is 5'9''. 

The **HexaBodyPlayer4.Calibrate** function should be called via a UI you provide to your player. After the calibration function executes you should persist the Camera's local y position to be reused when the player restarts your game.

The **HexaBodyPlayer4.CalibrateHeight** function should be called passing in the value you stored when the player resumes their game in the future.

Naturally if the player's play space changes, they will have to recalibrate.

### Sit / Standing Mode

The height calibration runs in two different modes:
1. Sitting - the Camera rig will lower / raise depending on the difference between the 'Eye Height' field and the height of the Camera to bring the in game player to it's standing pose.
1. Standing - The Camera's parent, named 'Scaler', will scale up or down depending on the height. 
    1. Shorter players would scale down and Taller players will scale up.
    1. This uniformly scales the controller and camera tracking which may not be 100% accurate, but close enough without Bonelab's level of engineering.

> [!TIP]
> It would be wise to offer fine tuning over the saved height calibration like Boneworks did. By giving 1 CM up / down adjustment buttons.

### Debug Height Calibration Helpers

The following fields on the HexaBody component can help with height calibration while testing. Even though the included code can save and restore height using these fields, it is strongly advised you create your own height saving and reloading mechanism as mentioned in [Height Calibration](#height-calibration).

CalibrateHeightOnStart - if enabled the calibration function will execute once the headset has moved past some small threshood. If 'SaveCalibrationHeight' is enabled, the previous stored height will be used to calibrate.

'SaveCalibrationHeight' - saves height calibration whenever Calibrate is executed.

The EnableDebugCalibrationButton fields on the HexaBodyInputs component allows the Recalibrate Key (default 'R') and 'X' button on the Left controller (Menu for WMR devices) for rapid recalibration during test cycles.

:::image type="content" source="../../images/hexadebugkeys.PNG" alt-text="str":::

The UI in the Hurricane integration scene has examples for height Calibration which change the Sit / Stand mode, and execute the Calibration function mentioned in [Height Calibration](#height-calibration).


# How do I change the height of my player?

The player cannot be scaled, therefore if you want to try and make a taller or shorter player changes these fields:

1. Eye Height - height to the eyes of the player to match with the HMD height.
    1. Change this to make your player shorter or taller
1. Player Waist Height - the pelvis is placed above the locoball by this distance.
    1. Crouch settings are a percentage of this height.
1. Colliders
    1. Chest Capsule Collider - height is controlled in the UpdateChest function, you can change the radius.
    1. Knee Capsule Collider - height is controlled in the UpdateLegCollider function, you can change the radius.
    1. Head Sphere Collider - you can change the radius.
    1. Loco Sphere Collider - you can change the radius.
        1. Fender Collider needs to be slightly larger than the Loco Sphere
            1. Adjust the Bumper offset field which raises the Fender - some trial and error required to prevent rolling up vertical objects. The point of the fender is to prevent rolling up walls, but still allow ground rolling.
        1. Loco and Fender collider radius are cached on awake, - if you change it at runtime you need to modify the code to recache your change. The jumping left lift sequence shrinks and restores the radius.