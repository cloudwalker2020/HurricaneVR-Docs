# Sockets

The [HVRSocket](xref:HurricaneVR.Framework.Core.Grabbers.HVRSocket) component is useful for snapping objects into place for building things like inventories.

- Sockets require a subclass of [HVRSocketFilter](xref:HurricaneVR.Framework.Core.Sockets.HVRSocketFilter) that will determine if a grabbable object is allowed.
  - Multiple socket filters can be applied to a socket. 
  - By default multiple filters run in 'AND' mode where all filters must be valid. To change to OR mode set the 'Filter Condition' field to OR. Then the object is allowed as long as one of the filtes IsValid method returns true.
- Each [HVRGrabbable](xref:HurricaneVR.Framework.Core.HVRGrabbable) requires a subclass of [HVRSocketable](xref:HurricaneVR.Framework.Core.Sockets.HVRSocketable) that has a matching filter to validate it.
  - One [HVRSocketable](xref:HurricaneVR.Framework.Core.Sockets.HVRSocketable) can be assigned to a grabbable object.

## Framework Provided Filters / Socketables

### Scriptable Object Based Filtering

The [HVRTagSocketFilter](xref:HurricaneVR.Framework.Core.Sockets.HVRTagSocketFilter) and [HVRTagSocketable](xref:HurricaneVR.Framework.Core.Sockets.HVRTagSocketable) pair are used in the examples scenes for the inventory and holster sockets.\
They provide the easiest solution to get started with socket filtering for both programmers and non programmers.\
Code validation is done using bitwise integer masking which is extremely performant.

Both components accept [HVRSocketableTags](xref:HurricaneVR.Framework.Core.Sockets.HVRSocketableTags) where you can define 32 categories of objects in the editor.\
After assigning the 'Tags' field on the Filter / Socketable, a multi-select dropdown will appear allowing you to assign multiple tags to the Filter and Socketable.\
Create your own: Assets -> Create -> HurricaneVR -> Socketables\
Be sure to File -> Save or CTRL+S to save scriptable object changes after editing them in the inspector.

### Grabbable Inclusion Filtering

The [HVRGrabbableSocketFilter](xref:HurricaneVR.Framework.Core.Sockets.HVRGrabbableSocketFilter) filter is used to filter specific grabbable objects that exist in your scene or prefab. This is used on the demo XR Rigs on the shoulder socket that holds the backpack.\
Any amount of grabbable objects can be assigned to the 'Valid Grabbables' field.

### Grabbable Exclusion Filtering

The [HVRGrabbableSocketExcluder](xref:HurricaneVR.Framework.Core.Sockets.HVRGrabbableSocketExcluder) can be used to allow every socketable EXCEPT the grabbables assigned to the component.

### Others

The rest of the included filters are deprecated due to the addition of the [Tag Based Filtering](#scriptable-object-based-filtering) and may be removed in a future update.

[HVRStringSocketFilter](xref:HurricaneVR.Framework.Core.Sockets.HVRStringSocketFilter) + [HVRStringSocketable](xref:HurricaneVR.Framework.Core.Sockets.HVRStringSocketable)\
[HVREnumSocketFilter](xref:HurricaneVR.Framework.Core.Sockets.HVREnumSocketFilter`1) + [HVREnumSocketable](xref:HurricaneVR.Framework.Core.Sockets.HVREnumSocketable`1)\
[HVREnumFlagsSocketFilter](xref:HurricaneVR.Framework.Core.Sockets.HVREnumFlagsSocketFilter`1) + [HVREnumFlagsSocketable](xref:HurricaneVR.Framework.Core.Sockets.HVREnumFlagsSocketable`1)

## Socketable Orientation

Socketable objects are parented to the object and their transform values are reset. If the Socketable has it's 'Socket Orientation' field assigned to a child transform, the local position and rotation will be pulled from that transform and aligned with the socket object axes. The grabbable objects in the example scene have these orientation overrides set as an example.

If a socketable object is allowed into two different socket types, it's possible you will need to write custom orientation logic into one of the socket components. The DemoHolster socket subclass used in the example scene can be used as a guide. The small weapons (knife and gun) have DemoHolsterOrientation components with a Transform override that will align the socketable axis with the socket axis.

The below code snippet shows the two virtual methods that the DemoHolster overrides from the [HVRSocket](xref:HurricaneVR.Framework.Core.Grabbers.HVRSocket) class.

```csharp
protected override Quaternion GetRotationOffset(HVRGrabbable grabbable)
{
    var orientation = grabbable.GetComponent<DemoHolsterOrientation>();
    if (orientation && orientation.Orientation)
        return orientation.Orientation.localRotation;
    return base.GetRotationOffset(grabbable);
}

protected override Vector3 GetPositionOffset(HVRGrabbable grabbable)
{
    var orientation = grabbable.GetComponent<DemoHolsterOrientation>();
    if (orientation && orientation.Orientation)
        return orientation.Orientation.localPosition;
    return base.GetPositionOffset(grabbable);
}
```

## Socketable Scaling

Each [HVRSocket](xref:HurricaneVR.Framework.Core.Grabbers.HVRSocket) has the option 'Scale Grabbable' which will automatically scale socketable objects by their Mesh Renderer bounding box sizes.

The localScale will be set to the 'Size' field divided by the longest bounding box axis length.

The [Scale Override](xref:HurricaneVR.Framework.Core.Sockets.HVRSocketable.ScaleOverride) which should reference a disabled Box Collider for sizing can be used to override the Mesh Renderer Bounding Box.

Skinned Mesh Renderer based socketables must use [Scale Override](xref:HurricaneVR.Framework.Core.Sockets.HVRSocketable.ScaleOverride), the Bow in the example scene uses this.

## Hover Actions

Each [HVRSocket](xref:HurricaneVR.Framework.Core.Grabbers.HVRSocket) can have any number of [HVRSocketHoverAction](xref:HurricaneVR.Framework.Core.Sockets.HVRSocketHoverAction) assigned to the ‘Hover Actions’ or ‘Hand Grab Actions’ fields.

The inventory sockets in the example scene have Hover Actions built to mimic Walking Dead: Saints and Sinners. They scale based on hand proximity and change to either green or red based on whether or not the socketable is allowed.

- HoverActions execute when the socket detects a [HVRGrabbable](xref:HurricaneVR.Framework.Core.HVRGrabbable) in it's [HVRGrabbableBag](xref:HurricaneVR.Framework.Core.Bags.HVRGrabbableBag)
- HandGrabActions execute when the socket is hovered by the [HVRHandGrabber](xref:HurricaneVR.Framework.Core.Grabbers.HVRHandGrabber) .

To create your own actions, subclass [HVRSocketHoverAction](xref:HurricaneVR.Framework.Core.Sockets.HVRSocketHoverAction) and override the following methods.

```csharp
public abstract void OnHoverEnter(HVRSocket socket, HVRGrabbable grabbable, bool isValid);
public abstract void OnHoverExit(HVRSocket socket, HVRGrabbable grabbable, bool isValid);
```
