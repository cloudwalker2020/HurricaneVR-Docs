# Inputs

HVR reads inputs from SteamVR, OpenXR (Input system), or UnityXR depending on the XR Plugin chosen. Be sure to read through [Scene Setup](scenesetup.md#scene-setup) first for required scene components.\
Polled during the Update phase by HVRController class and subclasses. 

### Controller Access

```csharp

//Access Controller classes from anywhere.
HVRInputManager.Instance.RightController;
HVRInputManager.Instance.LeftController;

```

### Available Fields

The following fields are available on the HVRController objects (depending on controller type).\
The HVRButtonState structs are used to determine if the button is pressed, just pressed, or just released.

```csharp

public struct HVRButtonState
{
    public bool Active;
    public bool JustActivated;
    public bool JustDeactivated;
    public float Value;
}

public HVRButtonState GripButtonState;
public HVRButtonState TriggerButtonState;
public HVRButtonState PrimaryButtonState;
public HVRButtonState SecondaryButtonState;
public HVRButtonState MenuButtonState;
public HVRButtonState PrimaryTouchButtonState;
public HVRButtonState SecondaryTouchButtonState;
public HVRButtonState JoystickButtonState;
public HVRButtonState TrackpadButtonState;

public HVRButtonState JoystickTouchState;
public HVRButtonState TrackPadTouchState;
public HVRButtonState TriggerTouchState;
public HVRButtonState ThumbTouchState;

public HVRButtonState TriggerNearTouchState;
public HVRButtonState ThumbNearTouchState;

public HVRButtonState TrackPadUp;
public HVRButtonState TrackPadLeft;
public HVRButtonState TrackPadRight;
public HVRButtonState TrackPadDown;

public Vector2 JoystickAxis;
public Vector2 TrackpadAxis;

public bool PrimaryButton;
public bool SecondaryButton;
public bool JoystickClicked;
public bool TrackPadClicked;
public bool MenuButton;
public bool PrimaryTouch;
public bool SecondaryTouch;

public float Grip;
public float GripForce;
public float Trigger;

public bool ThumbTouch;
public bool TriggerTouch;

```

### Controller Type

For PCVR, use the following HVRController Properties to determine the controller type. Your last else statement can handle Oculus / standard type controllers.

```csharp
public bool Knuckles => ControllerType == HVRControllerType.Knuckles;
public bool WMR => ControllerType == HVRControllerType.WMR;
public bool Vive => ControllerType == HVRControllerType.Vive;
```

### Controller Hand

```csharp

// Left or Right
public HVRHandSide Side { get; set; }

```




## HVRPlayerInputs
This component (On PlayerController object by default) collects device inputs for use by the player controller, teleporter, and hand grabbing systems. It's designed to be subclassed if the user wants to override which buttons drive specific actions for various device types.

> [!IMPORTANT]
> Update the component reference on both HVRHandGrabbers located on the Left and Right hand objects if replaced with a subclass.

## Accessing Controller From Grabbable

With a reference to a grabbable component, the below can be used to access the controller reference for each hand holding the object.

```csharp

for (var i = 0; i < Grabbable.HandGrabbers.Count; i++)
{
    var hand = Grabbable.HandGrabbers[i];
    var controller = hand.Controller;
}

```