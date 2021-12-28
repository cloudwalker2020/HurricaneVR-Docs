# Unity 2019 Legacy VR

As mentioned in the [Project and Packages Setup](setup.md#project-and-packages-setup), Legacy VR  is no longer viable for Oculus store builds. This setup process is only to be used if you are targeting PCVR via SteamVR and using Unity 2019.4 LTS.

1. Install OpenVR Desktop v2.0.5 from the Package Manager
1. Install Package “XR Legacy Input Helpers". This contains the HMD and Controller tracking components.
1. Open Project Settings (Edit → Project Settings → Player).
    - Virtual Reality Supported (checked)
    - OpenVR top of the list

:::image type="content" source="../images/legacy_vr.png" alt-text="legacyvr":::