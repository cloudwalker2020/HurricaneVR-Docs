# Project and Packages Setup

- Import the HurricaneVR Asset from the Unity Package Manager before proceeding.
- Make sure TextMesh Pro is installed and updated to the latest version for the example scenes.

## Oculus Store Builds

- [Oculus dev article on deprecation of the Unity 2019 Legacy Oculus SDK](https://developer.oculus.com/blog/oculus-all-in-on-openxr-deprecates-proprietary-apis/)
- Install [XR Plugin Management](#xr-plugin-management) with either the Oculus XR Plugin or the OpenXR Plugin.
- [Legacy SDK](#unity-2019-legacy-vr-sdks) is only allowed by Oculus with a waiver according to their article.

## PCVR Builds

Choose between using the SteamVR plugin or the new Unity OpenXR Plugin depending on what Unity version you want to use.\
Keep in mind Valve Knuckles finger tracking is not supported yet by Unity OpenXR and requires SteamVR plugin to work correctly.

- Unity 2019:  [Legacy SDK](#unity-2019-legacy-vr-sdks) + [SteamVR Setup](#steamvr)
- Unity 2019 and above: [XR Plugin Management](#xr-plugin-management) + [SteamVR Setup](#steamvr)
- Unity 2020.3 and above [XR Plugin Management](#xr-plugin-management) + OpenXR 1.3



## XR Plugin Management

Install the XR Plugin Management package from the Package Manager or the Project Settings window.

:::image type="content" source="../images/xr_plugin_management.png" alt-text="xr plugin":::

- Install the following packages from the Package Manager depending on your target platforms.
XR Plugin Management
Oculus XR Plugin
Windows XR Plugin
OpenXR Plugin 1.3 or higher. (2020.3+)
SteamVR Plugin (from the asset store)
The recent version of this asset installs the OpenVR XR Plugin Loader.
Follow the SteamVR setup steps below.

Enable the Plug-in Providers under ProjectSettings - XR Plugin-Management

## SteamVR


## Unity 2019 Legacy VR SDKs

1. Install OpenVR Desktop v2.0.5 from the Package Manager
1. Install Package “XR Legacy Input Helpers". This contains the HMD and Controller tracking components.
1. Open Project Settings (Edit → Project Settings → Player).
    - Virtual Reality Supported (checked)
    - OpenVR top of the list

:::image type="content" source="../images/legacy_vr.png" alt-text="legacyvr":::