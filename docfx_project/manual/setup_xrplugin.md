# XR Plugin Management

1. Install the XR Plugin Management package from the Package Manager or the Project Settings window.
1. Install the following packages from the Package Manager depending on your target platforms.
    1. Oculus: Oculus XR Plugin or OpenXR XR Plugin
    1. PCVR: OpenXR XR Plugin 1.3+ or [SteamVR Plugin](https://assetstore.unity.com/packages/tools/integration/steamvr-plugin-32647)
1. Enable the Plug-in Providers under Edit -> ProjectSettings -> XR Plugin-Management
    1. Oculus and/or OpenVR Loader OR OpenXR

:::image type="content" source="../images/xr_plugin_management.png" alt-text="xr plugin":::

:::image type="content" source="../images/xr_plugin_projectsettings.png" alt-text="xrplugin":::

## OpenXR Plugin 

Make sure to expand the OpenXR Plugin so that you can find version 1.3 and higher. These are required for haptics to work and your project will not compile without the correct version.

:::image type="content" source="../images/openxr_otherversions.PNG" alt-text="open":::

:::image type="content" source="../images/openxr_13.PNG" alt-text="o":::

> [!IMPORTANT]
> When using OpenXR, be sure to use the OpenXR rig variants as the device components are different from older versions: [XR Rigs](scenesetup.md#xr-rigs)

