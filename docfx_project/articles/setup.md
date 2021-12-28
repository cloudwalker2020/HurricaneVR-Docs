# Project and Packages Setup

- Import the HurricaneVR Asset from the Unity Package Manager before proceeding.
- Make sure TextMesh Pro is installed and updated to the latest version for the example scenes.
- Setup your Unity VR environment based on the below, then proceed to setup your [Project Settings](setup_project.md#project-setup).

## Oculus Store Builds

- [Oculus dev article on deprecation of the Unity 2019 Legacy Oculus SDK](https://developer.oculus.com/blog/oculus-all-in-on-openxr-deprecates-proprietary-apis/)
- Install [XR Plugin Management](setup_xrplugin.md#xr-plugin-management) with either the [Oculus XR Plugin](https://docs.unity3d.com/Packages/com.unity.xr.oculus@2.0/manual/index.html) or the [OpenXR Plugin](https://docs.unity3d.com/Packages/com.unity.xr.openxr@1.3/manual/index.html).
- [Legacy SDK](setup_legacyvr.md#unity-2019-legacy-vr) is only allowed by Oculus with a waiver according to their article.

## PCVR Builds

Choose between using the [SteamVR Plugin](https://assetstore.unity.com/packages/tools/integration/steamvr-plugin-32647) or [OpenXR Plugin](https://docs.unity3d.com/Packages/com.unity.xr.openxr@1.3/manual/index.html) depending on what Unity version you want to use.\
Keep in mind Valve Knuckles finger tracking is not supported yet by Unity OpenXR and requires SteamVR plugin to work correctly.

- Unity 2019:  [Legacy SDK](setup_legacyvr.md#unity-2019-legacy-vr) + [SteamVR](setup_steamvr.md#steamvr)
- Unity 2019 and above: [XR Plugin Management](setup_xrplugin.md#xr-plugin-management) + [SteamVR](setup_steamvr.md#steamvr)
- Unity 2020.3 and above [XR Plugin Management](setup_xrplugin.md#xr-plugin-management) + [OpenXR](https://docs.unity3d.com/Packages/com.unity.xr.openxr@1.3/manual/index.html) 1.3+
