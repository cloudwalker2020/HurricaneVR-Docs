# Grabbable Detection

The [HVRHandGrabber](xref:HurricaneVR.Framework.Core.Grabbers.HVRHandGrabber) and [HVRForceGrabber](xref:HurricaneVR.Framework.Core.Grabbers.HVRForceGrabber) both use  [HVRTriggerGrabbableBag](xref:HurricaneVR.Framework.Core.Bags.HVRTriggerGrabbableBag) components to detect grabbable objects.



[HVRGrabbable](xref:HurricaneVR.Framework.Core.HVRGrabbable) require colliders to be detected.

If your colliders are not on the same object as the [HVRGrabbable](xref:HurricaneVR.Framework.Core.HVRGrabbable) component, you will need to hint the grab system how to locate your grabbable component.

1. Add a [HVRGrabbableChild](xref:HurricaneVR.Framework.Core.HVRGrabbableChild) to the child objects that have colliders on them.
    1. Optionally set the Parent Grabbable field to the linked [HVRGrabbable](xref:HurricaneVR.Framework.Core.HVRGrabbable) object. If empty it will use the first parent grabbable it finds.
1. Open [HVRSettings](hvrsettings.md#grab-detection) and enable one or both at a global level if you wish, keeping in mind this applies to every collider the trigger system comes in contact with.
    1. Use Attached Rigid Body: the detected collider will use it's attached rigid body to locate the grabbable, since the grabbable should be on the same object as a rigidbody.
    1. Component In Parent Fallback: finds the first [HVRGrabbable](xref:HurricaneVR.Framework.Core.HVRGrabbable) that is a parent of the collider

> [!NOTE]
> The [RaycastLayermask](xref:HurricaneVR.Framework.Core.Grabbers.HVRHandGrabber.RaycastLayermask) field defines what layers the ray cast will hit for grabbable detection and line of sight testing. This field will need to be updated whenever you add additional layers for your environment or grabbable objects.

## Notes

- Subclasses of [HVRGrabbableBag](xref:HurricaneVR.Framework.Core.Bags.HVRGrabbableBag) are used to detect objects so that they can be grabbed.
- Each [HVRGrabberBase](xref:HurricaneVR.Framework.Core.Grabbers.HVRGrabberBase) needs at least one of these assigned.
  - If there are multiple assigned to a grabber, objects are given priority based on the index of the bag in the bag list.
  - Lower index is higher priority.
- Objects “in the bag” are sorted by their distance to the grabber to determine which one should be grabbed.
- If you wish you can subclass and extend the existing components to customize your grab detection system.