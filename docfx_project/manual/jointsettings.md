# [HVRJointSettings](xref:HurricaneVR.Framework.Core.ScriptableObjects.HVRJointSettings)

Scriptable object used to store and apply values to [Configurable Joints](https://docs.unity3d.com/Manual/class-ConfigurableJoint.html).

Used by the [HVRJointHand](xref:HurricaneVR.Framework.Core.Player.HVRJointHand) component on the [Physics Hands](rig/physicshands.md#physics-hands) to set the default hand strength.

Used by the [Hand Grabber](hands.md#hand-grabber) that is in "Pull Mode", the joint is created to pull the object to the hand with physics.

[HVRGrabbable](xref:HurricaneVR.Framework.Core.HVRGrabbable) provides override fields for:
- The joint between the hand rigidbody and the held object
- The strength of the hand (one or two hand overrides).
- The pull joint created that pulls the object to the hand


