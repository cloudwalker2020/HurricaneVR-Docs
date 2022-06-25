# Player Controller

The rig included with the asset makes use of Unity's [CharacterController](https://docs.unity3d.com/ScriptReference/CharacterController.html) component. It's important to note this is the most basic of movement providers, it is not a rigidbody and behaves like a massless object.
 
Games made using this will be limited to basic locomotion used in games like Alyx and Walking dead where objects do not collide with the player as they can easily push the player around.

If you want to build a game like Boneworks or Blade and Sorcery, then [HexaBodyVR](https://assetstore.unity.com/packages/tools/physics/hexabody-vr-player-controller-185521) will work better in this regard.

## [HVRPlayerController](xref:HurricaneVR.Framework.Core.Player.HVRPlayerController)

The main component that drives the [CharacterController](https://docs.unity3d.com/ScriptReference/CharacterController.html) using smooth locomotion with smooth / snap turning options. Disable for teleporting only.

## [HVRTeleporter](xref:HurricaneVR.Framework.Core.Player.HVRTeleporter)

Used to teleport the player with Alyx style line curve options, destination validation, "jump" and "fall" optional limits. If you do need laser based teleporting in your game you can disable the component.

Can be used to teleport the player with held objects programatically so be sure to leave this component as is if you need that functionality. Check 'scene_examples' for a demo of this.

## [HVRPlayerInputs](xref:HurricaneVR.Framework.ControllerInput.HVRPlayerInputs)

This component collects device inputs for use by the player controller, teleporter, and hand grabbing systems. It's designed to be subclassed if the user wants to override which buttons drive specific actions for various device types.

## [HVRTeleportCollisonHandler](xref:HurricaneVR.Framework.Core.Player.HVRTeleportCollisonHandler)

Handles moving hands and the objects they are holding after a teleport with post collision handling behaviours. 

The [AfterTeleportOption](xref:HurricaneVR.Framework.Core.Player.HVRTeleportCollisonHandler.AfterTeleportOption) lets you choose between "Sweeping" the hand toward the controller until it collides, or  "DisableCollision" which disables collision on the held object until it's clear of colliders (like Alyx). The object can't be dropped until it's clear.

The [ResetTarget](xref:HurricaneVR.Framework.Core.Player.HVRTeleportCollisonHandler.ResetTarget) field let's you define a point where the hand sweep begins from. On the included XRRig it's placed in the center of the CharacterController capsule.