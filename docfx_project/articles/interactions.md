# Grab System

## Grabbable Detection

The [HVRHandGrabber](xref:HurricaneVR.Framework.Core.Grabbers.HVRHandGrabber) and [HVRForceGrabber](xref:HurricaneVR.Framework.Core.Grabbers.HVRForceGrabber) both use  [HVRTriggerGrabbableBag](xref:HurricaneVR.Framework.Core.Bags.HVRTriggerGrabbableBag) components to detect grabbable objects.

Colliders and Triggers are required to go along with the [HVRGrabbable](xref:HurricaneVR.Framework.Core.HVRGrabbable) component.

If your colliders are not on the same object as the [HVRGrabbable](xref:HurricaneVR.Framework.Core.HVRGrabbable) component, you will need to hint the grab system how to locate your grabbable component.

1. Add a [HVRGrabbableChild](xref:HurricaneVR.Framework.Core.HVRGrabbableChild) to the child objects that have colliders on them.
    1. Optionally set the Parent Grabbable field to the linked [HVRGrabbable](xref:HurricaneVR.Framework.Core.HVRGrabbable) object. If empty it will use the first parent grabbable it finds.
1. Open HVRSettings and enable one or both at a global level if you wish, keeping in mind this applies to every collider the trigger system comes in contact with.
    1. Use Attached Rigid Body: the detected collider will use it's attached rigid body to locate the grabbable, since the grabbable should be on the same object as a rigidbody.
    1. Component In Parent Fallback: finds the first [HVRGrabbable](xref:HurricaneVR.Framework.Core.HVRGrabbable) that is a parent of the collider

### Notes

- Subclasses of [HVRGrabbableBag](xref:HurricaneVR.Framework.Core.Bags.HVRGrabbableBag) are used to detect objects so that they can be grabbed.
- Each [HVRGrabberBase](xref:HurricaneVR.Framework.Core.Grabbers.HVRGrabberBase) needs at least one of these assigned.
  - If there are multiple assigned to a grabber, objects are given priority based on the index of the bag in the bag list.
  - Lower index is higher priority.
- Objects “in the bag” are sorted by their distance to the grabber to determine which one should be grabbed.
- If you wish you can subclass and extend the existing components to customize your grab detection system.

## Hand Grabber

The [HVRHandGrabber](xref:HurricaneVR.Framework.Core.Grabbers.HVRHandGrabber)  components reside on the hand rigid body objects. It is important to note how the grab flow works.

The hand operates in "[Hand Grabs](#hand-grabs)" or “[Pull](#hand-pulls)” mode for physics based grabbing that use [Configurable Joints](https://docs.unity3d.com/Manual/class-ConfigurableJoint.html).

### Hand Grabs

The hand will move to the object to grab it and immediately create a [Final](#final-joint) strong joint with the object. After which the hand returns to the controller via physics.

This will happen if:

- HandGrabs is enabled on the [HVRHandGrabber](xref:HurricaneVR.Framework.Core.Grabbers.HVRHandGrabber).
- [HVRGrabbable](xref:HurricaneVR.Framework.Core.HVRGrabbable) is marked Stationary
- [HVRGrabbable](xref:HurricaneVR.Framework.Core.HVRGrabbable) is Joint based without a rigid body.
- The object being grabbed is already held with one hand.

### Hand Pulls

The grabbed object will be pulled towards the hand using the HVRJointSettings supplied in the “Pulling Settings” field.\
This is done this way to prevent grabbed objects from hitting surrounding objects with infinite force while it moves and rotates into position.

Each [HVRGrabbable](xref:HurricaneVR.Framework.Core.HVRGrabbable) can have this pull joint setting overridden, which should be done for objects greater than 2 mass.

### Final Joint

When [Hand Grabs](#hand-grabs) completes, or [Hand Pulls](#hand-pulls) has pulled the object close enough, a final "strong" [Configurable Joint](https://docs.unity3d.com/Manual/class-ConfigurableJoint.html) is created between the hand rigid body and the grabbable rigid body.

The settings of the joint can be overridden globally @ HVRSettings.DefaultJointSettings or per grabbable's [JointOverride](xref:HurricaneVR.Framework.Core.HVRGrabbable.JointOverride) field.

[HVRGrabbableChild](xref:HurricaneVR.Framework.Core.HVRGrabbableChild)
[HVRGrabberBase](xref:HurricaneVR.Framework.Core.Grabbers.HVRGrabberBase) 
[HVRHandGrabber](xref:HurricaneVR.Framework.Core.Grabbers.HVRHandGrabber) 
[HVRForceGrabber](xref:HurricaneVR.Framework.Core.Grabbers.HVRForceGrabber) 
[HVRTriggerGrabbableBag](xref:HurricaneVR.Framework.Core.Bags.HVRTriggerGrabbableBag)
[HVRGrabbable](xref:HurricaneVR.Framework.Core.HVRGrabbable)