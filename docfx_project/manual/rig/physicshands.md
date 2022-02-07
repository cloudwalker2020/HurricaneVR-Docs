# Physics Hands

The hands are driven using a PD controller. The implementation makes use of Unity's [Configurable Joint](https://docs.unity3d.com/Manual/class-ConfigurableJoint.html) to take advantage of the physics engines iterative nature and stability of simulation that joints allow. 

PD controllers are simply PID controllers that ignore the I component, if you want to learn more on the subject then check out this excellent video on the topic - [PID Control](https://www.youtube.com/watch?v=wkfEZmsQqiA).

## HVRJointHand

[HVRJointHand](xref:HurricaneVR.Framework.Core.Player.HVRJointHand) is a PD controller implementation that chases the target controller.

[JointSettings](xref:HurricaneVR.Framework.Core.Player.HVRJointHand.JointSettings) defines the default PD values used that controls the hand's strength.

 
### Max Distance

If distance between the hand and the controller is greater than [MaxTargetDistance](xref:HurricaneVR.Framework.Core.Player.HVRJointHand.MaxTargetDistance) or if the distance between [Anchor](xref:HurricaneVR.Framework.Core.Player.HVRJointHand.Anchor) (shoulder) and the hand is greater than [ArmLength](xref:HurricaneVR.Framework.Core.Player.HVRJointHand.ArmLength) one of the below is performed.

Set [MaxDistanceBehaviour](xref:HurricaneVR.Framework.Core.Player.HVRJointHand.MaxDistanceBehaviour) to determine what happens after max distance is breached.
- GrabbablePrevents - if you're holding an object then nothing happens.
- GrabbableDrops - the object you are holding is released, hand collision is disabled, then the hand smoothly returns to the controller.
- HandSweep - [HVRTeleportCollisonHandler](xref:HurricaneVR.Framework.Core.Player.HVRTeleportCollisonHandler) is used to try and safely bring the hand and held object (if any) to a position between the player and the controller.

> [!TIP]
> [Anchor](xref:HurricaneVR.Framework.Core.Player.HVRJointHand.Anchor) and [ArmLength](xref:HurricaneVR.Framework.Core.Player.HVRJointHand.ArmLength) are useful if your avatar has arms (with or without a full body) to keep the hand from going further than it should.

> [!NOTE]
> [OverrideMaxDistanceBehaviour](xref:HurricaneVR.Framework.Core.HVRGrabbable.OverrideMaxDistanceBehaviour) and
[MaxDistanceBehaviour](xref:HurricaneVR.Framework.Core.HVRGrabbable.MaxDistanceBehaviour) override this behaviour on a per object basis.


## HVRThrowingCenterOfMass

[HVRThrowingCenterOfMass](xref:HurricaneVR.Framework.Components.HVRThrowingCenterOfMass) holds transform points relative to the hand that represent the center of mass of the controller. To try and achieve solid throwing in VR, the center of mass of the controller is used in the final throwing calculation that converts angular velocity to linear velocity. This seems to work well since you're actually swinging your controller around in real life, and not the object that you are throwing in game.

> [!TIP]
> If you disagree with this approach, you can remove this component. The center of mass of the hand's rigidbody will instead be used to convert angular velocity to linear velocity when throwing.

## HVRRigidBodyOverrides

Used to override rigidbody properites of the hand.

Inertia Tensor Rotation is zeroed out to enable smooth rotation along all axis.

Inertia Tensor is set to a default value that feels good with the default joint settings. You may wish to adjust this if you want to control the torque required to rotate the hand.

## HVRHandStrengthHandler

Manages the strength applied to the hand that might be overriden by the grabbable objects. Used internally by the framework and can be ignored outside of debug use.

The current joint setting applied to the hand can be viewed here if you want to verify that your strength override is applied correctly.

Setting 'Always Updated Joint' to true will evaluate the settings in the active joint settings every frame, you can enable this while in play mode to modify the settings to test the affects of different PD controller values.

## HVRHandPhysics

Basic component that holds a reference to the hand's colliders, mostly used internally by the framework.