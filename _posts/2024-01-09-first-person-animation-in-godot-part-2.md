## First Person Animation in Godot - Part 2

This is the second blog post

---

### Setting up the base scene

The base scene is simple and consists of a few nodes:

- A Node3D that holds the other node, called `World`
- A standard Node that holds the world environment nodes. The world environment uses a HDRI as its sky texture.
- Directional light that simulates a sun
- A standard node that holds objects in the level, such as the ground and some boxes. These are CSG nodes, and don't contain any collision as it is not needed for this purpose.

![Scene_1](/img/godot/godot_scene_1.png)

The next step is to import the files to the project, you can drag and drop the `.glb` files in a folder. Make sure the texture is also present next to these files.

![Scene_2](/img/godot/godot_scene_2.png)

You can verify that the animations are working on the armature and gun, by opening the `.glb` files and playing the animation on the `AnimationPlayer` node.

![Scene_3](/img/godot/godot_scene_3.png)
![Scene_4](/img/godot/godot_scene_4.png)

Next we create a material resource that holds the texture for the arms and gun mesh. Create a new resource in your project folder and select `StandardMaterial3D`.

![Scene_5](/img/godot/godot_scene_5.png)

Assign the texture image to the `Albedo` of the material.

![Scene_6](/img/godot/godot_scene_6.png)
![Scene_7](/img/godot/godot_scene_7.png)

You are now done with setting up your assets, and are able to continue to setup the viewmodel in the scene!

### Setting up the viewmodel

First, split your viewport in to two screens. This will be needed later to position the gun properly and match it with the first person view.

![Scene_8](/img/godot/godot_scene_8.png)

Create an empty 3D scene and add a main Node3D called `PlayerViewModel`. Add the arms `.glb` file under this node, and make it local by right clicking the file -> Make Local.

![Scene_9](/img/godot/godot_scene_9.png)

Your hierarchy should now look similar to the following example, except for the socket bones.

![Scene_10](/img/godot/godot_scene_10.png)

Under the `Skeletal3D` node, add two `BoneAttachment3D` nodes and assign one to the camera bone, and one to the right hand bone. These attachments act as the sockets that will inherit the position and rotation of the parent bone.

![Scene_11](/img/godot/godot_scene_11.png)

WORK IN PROGRES...

### Next steps

This should allow you to test out viewmodel animations in Godot. In a future blog post, I will look into exporting multiple animations with one rig. If you have any recommendations / suggestions or other comments, please open a discussion on [GitHub](https://github.com/xandev133/xandev133.github.io/discussions)