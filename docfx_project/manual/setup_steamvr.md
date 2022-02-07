# SteamVR

Download and import the [SteamVR Plugin](https://assetstore.unity.com/packages/tools/integration/steamvr-plugin-32647) from the Unity Store.

## Hurricane Integration

1. Extract the SteamVR Integration located at /HurricaneVR/Framework/Integrations.
1. Press “Import” when prompted to import the Partial Input binding for ‘HVR’. If a second option comes up, choose “Replace”, not “Merge”
1. The SteamVR Input window should present itself, if not open this window via your toolbar at : Window → SteamVR Input
1. At the bottom of the SteamVR Input window, locate and press the “Save and generate” button.
1. Add HVR_STEAMVR to your project setting scripting define symbols or by using Tools → HurricaneVR → Setup
    1. Wait a moment as the imported code becomes compiled.


:::image type="content" source="../images/steamvr_hvrsetup.png" alt-text="steamhvr":::
 
## Unity 2019

Because 2019 has access to Legacy and XR Plugin Management, you may receive this prompt after you import the plugin.\
At this point you can decide whether to remain with Legacy OpenVR or update to XR Plugin (OpenVR)

:::image type="content" source="../images/steamvrlegacy.png" alt-text="steamlegacy":::

If you decide to convert to XR Plugin and receive this prompt, be sure to press Ok so that it will clean out the Legacy packages for you, if you fail to do so then you must remove the old packages manually.
 
:::image type="content" source="../images/steamvr_xrplugin_warning.png" alt-text="steamxr":::