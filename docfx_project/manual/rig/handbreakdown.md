# Hand Breakdown

The following gives some context to the objects and their purpose as part of the default XR Rig and Hand prefabs.

## Joint Anchor

Anchor point for the [Configurable Joint](https://docs.unity3d.com/Manual/class-ConfigurableJoint.html) when attaching to a held object.

Should be placed closer to the hand's center of mass.

## Force Grabber

[HVRForceGrabber](xref:HurricaneVR.Framework.Core.Grabbers.HVRForceGrabber) pulls grabbable objects to the hand using physics forces.

- ForceGrabOrigin: Origin and direction of the line of sight raycast used by the force grabber.
- ForceGrabLaser: [HVRForceGrabberLaser](xref:HurricaneVR.Framework.Core.HVRForceGrabberLaser) using Line Renderer to draw the gravity gloves laser.
- ForceGrabberBags: [Grabbable Detection](../detection.md#grabbable-detection) triggers. Referenced by [GrabBags](xref:HurricaneVR.Framework.Core.Grabbers.HVRGrabberBase.GrabBags). Lower indices in the array have higher priority.

## OverlapSizer

Sphere collider that is used to position and size a call to [Physics.OverlapSphere](https://docs.unity3d.com/ScriptReference/Physics.OverlapSphereNonAlloc.html) to check if a recently released object is still close to the hand after a [OverlapTimeout](xref:HurricaneVR.Framework.Core.HVRGrabbable.OverlapTimeout) amount of time passes.

## Socket Bag

Trigger collider used with [HVRSocketBag](xref:HurricaneVR.Framework.Core.Bags.HVRSocketBag) to detect sockets in range of the hand.

Used by the [HVRHandGrabber](xref:HurricaneVR.Framework.Core.Grabbers.HVRHandGrabber) to determine the closest valid socket to grab objects out of if allowed.

## Grabbable Bag

Trigger collider used to detect grabbable objects. Can be resized and repositioned if you like. [Read about Grabbable Detection](../detection.md#grabbable-detection).

## Teleport

Used by the [HVRTeleporter](xref:HurricaneVR.Framework.Core.Player.HVRTeleporter) to aim and position the start of the teleport line.

## CenterOfMasses

Used by the [HVRThrowingCenterOfMass](physicshands.md#hvrthrowingcenterofmass) component to define device specific center of mass points to aid in throwing calcs.

## UIPointer

Holds the disabled camera, line renderer, and HVRUIPointer component used by the HVRInputModule that allows interactions with world space canvases.

Transform defines the position and direction (forward vector) of the pointer.

## HandRayCastOrigin

Raycasts are performed to determine if the object in the Grabbable Bag trigger can be seen by the hand to prevent grabbing objects through world geometry. The position of this transform is the origin of the raycast.

## FallbackPoser

Holds a HVRHandPoser component that defines a hand pose to use when "Offset" grabbing, or if a valid grab point couldn't be found due to position and rotation restrictions defined on the grab point.

## Hand Grab Indicator

Holds the default grab indicator that positions itself on grab points when the hand is hovering and not yet holding an object.

## Hand Poses

Holds the poses that the Force Grabber uses when it's Hovering or Pulling an object toward the hand and the poses that the Hand Grabber use's when it's Hovering, Pulling, or Retrieving an object.

## Dynamic Grab Indicator

Optional grab indicator that positions itself on the grabbable object to show where the palm will land.

## Force Grab Indicator

Visual indicator that positions itself on the grabbable object when the Force Grabber Hover's an object.