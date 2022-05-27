# Custom Hand Setup

To use your own hand models, you will want to make sure that you have a pair of hands where one was mirrored from the other in the 3d modeling program. This will allow the hand to be mirrored rapidly in the hand poser editor.

If you have a single hand model you can follow this guide created by a fellow community user to created the second hand.

> [!Video https://www.youtube.com/embed/Hwgj7Z2_zLU]

## Hand Setup Wizard

If you have a set of hands that are mirrorable, you can make use of the hand setup wizard which automates a majority of the component and field setup.

:::image type="content" source="../images/custom_hand_menu.PNG" alt-text="customhandtoolbar":::

1. Place the hand's as a child of the same object, making sure the fingers are pointing along the forward (blue) axis of the parent object.

:::image type="content" source="../images/handwizard_empty_go.PNG" alt-text="handemptygo":::

:::image type="content" source="../images/handwizard_hand_start.PNG" alt-text="start":::

2. Assign the hand root transforms.
3. Assign the Rig root that these hands will attach to. Any included rig will work, including the HexaBody integration rigs.

:::image type="content" source="../images/handwizard1.PNG" alt-text="hw1":::

4. Most models (should) have a common parent transform of the finger bones. Locate this and assign as in the image above.

:::image type="content" source="../images/handwizard_finger_parent.PNG" alt-text="hwfp":::

5. The standard order for finger bones are Index, Middle, Pinky, Ring, Thumb. If your model does not follow this order, adjust the order using the drop downs.
6. Assign the number of bones that each finger has.
7. If there are non bone transforms between the assigned "Finger Parent" and the first bone of the finger, increase the "Root Offset" count for each of these.
    1. This most likely won't be the case unless the hand designer is doing some weird stuff..
8. After all fields are assigned, press Setup.

10. Upon pressing Setup, a new transform named "Palm" is added to each hand. Place it in the center of the palm just on the surface of the mesh with the forward axis facing out at a 90 degree angle from the palm surface as in the image below. Make sure to do this for both hands.

:::image type="content" source="../images/handwizard_palm.PNG" alt-text="palm":::

11. Take note of the Tip transforms added to each end bone.

:::image type="content" source="../images/handwizardtips.PNG" alt-text="tips":::

12. Move each Tip transform to the center of the last bone as in the below image.

:::image type="content" source="../images/hand_wizard_tip.PNG" alt-text="tip placement":::

13. At this point your editor should look like the below image. The progress tracker simply controls what view is currently seen. If you need to go back and redo a previous step simply uncheck the boxes from bottom to top.
14. The hands should still be oriented facing forward on their dummy game object. Press Detect Mirror. This will snapshot the forward and up vectors of each bone for pose mirroring.
15. After pressing Detect Mirror the option to "Start Mirroring" presents itself. This will let you test the mirroring of the hand bones.
 :::image type="content" source="../images/handwizardmirror.PNG" alt-text="hwmirror":::
16. Pressing Mirror Test will clone the hands. Test mirroring by moving the Right Hand root, and the right hand bones. The left bone should mirror and match.
    1. If mirroring for the thumbs failed, uncheck 'Mirror Detected', force the thumbs to align more closely with the forward vector of the dummy parent object, and try detecting mirror again.
:::image type="content" source="../images/handwizard_mirrortestobjects.PNG" alt-text="mtesto":::

:::image type="content" source="../images/handwizardmirrortest.PNG" alt-text="mtest":::
17. Once satisfied the mirroring is working, press Stop Mirroring. Then press 'Setup Rig References': this will replace the rig references to the components added to the new hands for you. The below screen will present itself.

:::image type="content" source="../images/handwizard_poseview.PNG" alt-text="pv":::

18. Press 'Auto Setup Prefab / HVR Settings. This will create prefabs of the hand models in the root folder of the project (after the entire process is done feel free to relocate them), and update the HVRSettings scriptable object with the hand prefabs which is required for the posing system. If you locate your HVRSettings (search HVRSettings in the project search bar) you should now see the below fields populated. The prefabs are named the same as the hand model root's game object name.
    1. While in HVRSettings you can choose a folder in your project for pose saving by pressing 'Chose Poses Directory' at the bottom of the inspector.

:::image type="content" source="../images/handwizard_hvrsettings.PNG" alt-text="hw":::

19. Press 'Create Hand Poser'. This will create a new game object with a HVRHandPoser component on it. Choose either hand and enable the preview for it in the hand poser editor. Proceed to create three poses:
    1. Relaxed Pose: How the hand will look when you are not holding anything
    2. Fist Pose: Used by the hand animator when not holding anything and driven via capacitive finger curls. Also used by the dynamic poser.
    3. Open Pose: Used by the dynamic poser as the starting pose that interpolates towards the fist pose. A wide opened hand works best here.
    4. The posing and save process is the same as outlined in this tutorial video : [Hand Posing Tutorial](https://youtu.be/HZQ6QdMmZ34).
    1. After the poses are created, assign them in their respective fields and press 'Setup Poses'
        1. The wizard will apply the pose field overrides automatically to the prefab objects in v2.8.6 and higher. In v2.8.5 and below you will need to apply the pending prefab overrides on the hand model prefabs.

:::image type="content" source="../images/handwizard_assignposes.PNG" alt-text="assign":::

20. At this point you will want to add colliders to your hand models, how you do this is up to you. There are some capsule collider helper buttons on the HVRPosableHand component located on the hand root. It will try and fit them based on the bone structure, but might need some massaging after adding.

:::image type="content" source="../images/handwizard_capsules.PNG" alt-text="cap":::

21. The final step is to set the default position and rotation of the hand. Locate the hands on the physic hand objects. They were placed there by the setup process. You can use the existing rig hand as a guide. Afterwards I suggest going into play mode and placing the hand how you want it, copying the transform values out of play mode and back into edit mode. Once done you can remove the old hand model from the rig.

:::image type="content" source="../images/handwizard_findhand.PNG" alt-text="hand":::


