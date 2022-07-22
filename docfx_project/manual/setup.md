# Project and Packages Setup

- Import the HurricaneVR Asset from the Unity Package Manager before proceeding.
- Make sure TextMesh Pro is installed and updated to the latest version for the example scenes. 
- Setup your Unity VR environment based on the below, then proceed to setup your [Project Settings](setup_project.md#project-setup).
- Optional Use Empty Template Projects
    - https://github.com/cloudwalker2020/HurricaneTemplate_2021_OpenXR
    - https://github.com/cloudwalker2020/HurricaneTemplate_2021_SteamVR

# XR Plugin Management

1. Install the XR Plugin Management package from the Package Manager or the Project Settings window.
1. Install the following packages from the Package Manager depending on your target platforms.
    1. **Oculus**: Oculus XR Plugin
        1. OpenXR XR Plugin also works but I feel that Oculus XR Plugin currently is better for Oculus devices.
    1. **PCVR**: [SteamVR](setup_steamvr.md#steamvr) or OpenXR Plugin.
        1. Keep in mind Valve Knuckles finger tracking is not supported yet by Unity OpenXR and requires SteamVR plugin to work correctly.
1. Enable the Plug-in Providers under Edit -> ProjectSettings -> XR Plugin-Management
    1. Oculus and/or OpenVR Loader OR OpenXR

:::image type="content" source="../images/xr_plugin_management.png" alt-text="xr plugin":::

:::image type="content" source="../images/xr_plugin_projectsettings.png" alt-text="xrplugin":::

## OpenXR Plugin 

Make sure to expand the OpenXR Plugin so that you can find version 1.3 and higher. These are required for haptics to work and your project will not compile without the correct version.

Install the Interaction Profiles for the devices you want to support.

- G2 Support : https://developers.hp.com/omnicept-xr/blog/reverb-g2-tracking-openxr-unity?language=ko
- WMR Support: https://docs.microsoft.com/en-us/windows/mixed-reality/develop/unity/welcome-to-mr-feature-tool

:::image type="content" source="../images/openxr.PNG" alt-text="o":::

:::image type="content" source="../images/openxr_otherversions.PNG" alt-text="open":::

:::image type="content" source="../images/openxr_13.PNG" alt-text="o":::

> [!IMPORTANT]
> Select the Oculus OpenXR runtime if you are using Oculus devices. SteamVR blocks the left menu button on Oculus devices.
> Also as of July 2022 SteamVR broke Oculus devices anyway, read [here](https://forum.unity.com/threads/primary-button-on-quest-2-controllers-never-returns-true-when-pressed.1294833/#post-8214897)

> [!IMPORTANT]
> When using OpenXR, be sure to use the OpenXR rig variants as the device components are different from older versions: [XR Rigs](scenesetup.md#xr-rigs)