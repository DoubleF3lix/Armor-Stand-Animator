# Armor Stand Animator
Provides an interface for [Blockbench](http://blockbench.net/) to animate armor stands which is converted to a data pack.

## Usage
First, install the [plugin](https://www.blockbench.net/plugins/armor_stand_animator) via the Blockbench plugins store. Then, add both the "Create Armor Stand Model" and "Export Armor Stand Animation" actions to your toolbar. 

Next, create a new Blockbench project. You can use whatever format you like (Bedrock works best in my experience). Since you get 360 degrees of freedom in each axis, you can use the Generic Model format if you like. 

In any case, click the "Create Armor Stand Model" action to create a new armor stand. This will also import a basic texture for you. Then, in the "Animate" menu, create a new animation. Name it whatever you like, but make sure the snapping value is set to 20. If it's not 20, any keyframe time will be rounded up, which can create undesirable results. You can set the Loop Mode or the Start Delay if you wish. Note that "Hold On Last Frame" and "Play Once" do the same thing in the final data pack. Now, it's time to animate your armor stand. You can move the base `armor_stand` bone around to change the position of the armor stand (it teleports relative to its current position), and you can modify the rotation of any bone except you cannot modify the X or Z axis of the `armor_stand` bone. Changing the Y axis will edit the Rotation of the armor stand. To make this process easier, I highly recommend installing the [**Bakery**](https://www.blockbench.net/plugins/bakery) plugin. It turns the interpolated preview into real keyframes. Without these keyframes, the final animation will "skip" directly to the next keyframe. Simply select a starting keyframe, select an ending keyframe, and then use the "Bake Animations" action in the toolbar.

Now that you have a finished animation, use the "Export Armor Stand Animation" action. You can edit the following parameters:
- `Block/Unit Ratio` - This describes the ratio between Blockbench units and minecraft blocks. By default, 1 Blockbench unit is 1/16th of a minecraft block.
- `Time Scale` - This describes the scale your animation will play at. Setting this to `2` will make your animation play in half speed.
- `Pack Name` - This should follow normal namespacing conventions. This controls the namespace name of the exported animation. 
- `Entity Tag` - This controls the tag that the armor stand entity uses. Set this to something unique, or else the animation will start modifying things you didn't want it to. 

The plugin exports a namespace file, so just unzip the file into your data pack's `data` folder, and you're good to go. Make sure you run `function <pack_name>init` before starting to create the necessary objectives. This only needs to be run once. To summon the armor stand, run `function <pack_name>:create`. To start the animation, run `execute as @e[tag=<entity_tag>] run function <pack_name>:start`. This should work for multiple entities at once, and it's optimized to have a minimal impact on TPS. Note that TPS may be affected with several animations running at once. (Editing the rotation of limbs uses a `data merge` command, which can be quite taxing with quantity).

---

Found a bug? Create an [issue](https://github.com/DoubleF3lix/Armor-Stand-Animator/issues/new) on the GitHub repository.

Special thanks to vdvman1 for helping me optimize the data pack, and to many others in the [Minecraft Commands Discord](https://discord.gg/QAFXFtZ) for feedback. 