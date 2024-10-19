## Rigging FPS arms in Blender

---

### Prerequisites

- Blender (4 or higher)
- Some low poly arms model

### Goals

- Rig and skin the arm model
- Add bone constraints
- Add bone shapes
- Add controller bones

---

### Preparing the gun model

Make sure that the 3D cursor is centered to the world's origin by using `SHIFT + S` -> Cursor to world origin. In this example, I am rigging one arm to keep things simple, and to avoid over-information. Everything applies to the other side, which you can easily mirror by using symmetry.

Also consider the scale of the object and make sure all transforms are applied for position, rotation and scale. You generally want the arms in a T-pose. Additionally, it might be a good idea to keep iterations of the rigging proces so you can always go back. For example, keep the arm mesh in a separate .blend file. Then copy this file and add the armature.

---

### Adding the armature

When the arm mesh is centered, and you have applied the scale, you are ready to add a new armature. Press `SHIFT + A` -> Armature to add your first bone. Go into edit mode. In the bone properties tab (green bone icon), you can rename the bone to **root**. This will be the main bone. Every other bone will be a child of the root bone.

![rootbone](/img/rigging_fps_arms/1_armature_adding_root_bone.png)

While being in edit mode, select the root bone and duplicate it with `SHIFT + D`. Move this bone to match the upper arm, lower arm, and hand like so:

![armbones](/img/rigging_fps_arms/2_armature_adding_arm_bones.png)

**Tip: Pull the elbow slightly back, so there is a 'bend' in the arm. This will help the IK-solver later when adding constraints**

Make sure that the upper arm bone's parent is the root bone. You can confirm this in the bone tab under 'relations'. Visually there will also be a dotted line towards the root bone. The lower arm bone has to be a child of the upper arm bone, and the hand a child of the lower arm bone.

In order to make the rigging process easier, it is generally a good idea to enable certain viewport settings. You can do this by selecting the armature in edit mode. Go to object data properties (green running stick-figure icon), and tick all boxes under viewport display.

![settings](/img/rigging_fps_arms/3_viewport_settings.png)

**Tip: Use the 3D cursor to align the bones perfectly with the low-poly arm mesh. Select the mesh, go into edit mode, select a face, press SHIFT + S -> cursor to selected. Then go back to the arm rig in edit mode, select the bone head or tail, press SHIFT + S -> selection to cursor.**

The process above is repeated for the fingers aswell. The lower part of the finger will be a child of the hand bone. The middle part will be a child of the lower finger bone etc. After adding all the bones and naming them, and making sure they are aligned, you should have something like this:

Top-view:

![armature](/img/rigging_fps_arms/4_full_armature.png)

Side:

![armature_2](/img/rigging_fps_arms/4_full_armature_2.png)

Make sure to apply all transforms to the rig in object mode to avoid further issues.

---

### Adding controller bones

In this part of the guide we're going to add controller bones. Controller bones will not deform the object, and act as a visual aid to move the actual deform bones that we added in the previous part. The controller bones will have their own bone shape, to make it clear which parts of the rig can be moved.

Duplicate the following bones:

- upper arm (rename to upper_Ctrl_L, parent to root)
- hand (rename to hand_Ctrl_IK_L, parent to root)
- lower fingers (rename to fingername_Ctrl_L, parent all to hand)

Finally, we also need to add a pole target bone behind the elbow. This is the target that allows the arm to 'rotate'. See the image for an example. Make sure that in the bone properties the 'deform' checkbox is unticked / set to false.

![controllerbones](/img/rigging_fps_arms/5_adding_controller_bones.png)

**Tip: Select the controller bones, and go to viewport display. Set bone color to red / blue depending if it is the right or left arm.**

Next, select all your controller bones and assign them to a new bone collection. Note that if you are planning to rig two arms, you want two controller bone collections (for left and right).

![controllerbones](/img/rigging_fps_arms/5_adding_to_bone_collection.png)

Finally, we want to create bone shapes so the rig will look a bit cleaner. Add a new cube and UV-sphere and move them next to your rig.
Add them to a collection, and apply the transforms for both meshes.

![controllerbones](/img/rigging_fps_arms/5_bone_shapes.png)

In pose mode, select each bone and in the bone properties tab go to viewport display. Use the picker tool to select one of your meshes. Edit it so it surrounds the part of the arm that is controlled.

![controllerbones](/img/rigging_fps_arms/6_assigning_bone_shapes.png)

---

### Adding constraints

In this part of the guide we will add constraints to the bones so they can actually move.

---

### Adding a FPS camera

TODO

---

### Skinning

In this part of the guide we skin the arm mesh to the rig. This is the process where we assign parts of the mesh to a vertex group. A vertex group is then moved by moving the bone.