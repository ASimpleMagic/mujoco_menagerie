# asMagiClaw (MJCF)

asMagiClaw is a motor-driven two-finger gripper developed by the Design and
Learning Research Group. The two configurations share the same four-bar
linkage and rigid fingertip contact model.
[MagiClaw project and paper](https://arxiv.org/abs/2509.19169)

| Configuration | Workbench scene | Reusable model |
| --- | --- | --- |
| Gripper with robot-mount flange | `scene.xml` | `asmagiclaw.xml` |
| Handheld with handle, trigger, cold shoe, holder, and iPhone 12 Pro reference | `scene_handheld.xml` | `asmagiclaw_handheld.xml` |
| Handheld with six-axis pose controls | `scene_handheld_umi.xml` | `asmagiclaw_handheld.xml` |

## First-person view

Open the [handheld project in Studio](https://asimplemagic.com/?sample=asmagiclaw-handheld).
In the simulator, choose `iphone_12_pro_rear` under **Rendering → Camera**.
Choose **Free: tumble** to return to the orbit view. With the viewport focused,
`]` cycles through the camera options. The camera is fixed to the published
rear lens frame and faces the fingers in landscape orientation.

For the UMI-style workbench, select `scene_handheld_umi.xml` under **Entry model**
and choose **Apply**. Select `gripper_iphone_12_pro_rear` in the same camera menu.
Press **Run** and open **Inspector → Controls**. Use `handheld_x`, `handheld_y`, and `handheld_z`
for translation, and `handheld_roll`, `handheld_pitch`, and `handheld_yaw`
for rotation. Use `gripper_claw_beam` to move the fingers. Like the Menagerie
UMI scene, the gripper and its camera move together through six pose axes.

The simulated iPhone lens uses a 92° vertical perspective field of view,
approximately 120° diagonally in a 4:3 image. UMI's hardware uses a GoPro
fisheye lens and side mirrors.
[UMI in Menagerie](https://github.com/google-deepmind/mujoco_menagerie/tree/main/umi_gripper) ·
[UMI paper](https://umi-gripper.github.io/umi.pdf) ·
[iPhone 12 Pro specifications](https://support.apple.com/en-us/111875)

## Open and close the gripper

All three scenes provide `home` and `open` reset keyframes. In **Controls**,
set the jaw control to `1.10` rad to open the fingers or `-0.02` rad to close
them. The control is named `claw_beam` in the fixed-base workbenches. Adjust the
target gradually for smooth motion.

Use `asmagiclaw.xml` to attach the gripper to a robot. In the authored
model frame, +X points toward the fingers and +Z points up. `ft_frame` is the
original shell-origin reference, and `grasp_reference` is a nominal point
0.30 m forward of that origin.

## Model and validation

Six hinge coordinates describe the linkages. A joint equality synchronizes the
two driven beams, and two point equalities close the follower loops. The
mechanism has one independent motion. The position actuator is bounded to
±3 N·m. The printed parts use CAD-derived PLA mass and inertia estimates. The
handheld mount uses the published CAD transforms. The phone has the original
reference mesh, a 189 g mass, and box inertia from Apple's handset dimensions.
Bracket inertias use the source CAD estimates. The contact model treats the
MetaFinger surfaces as rigid. [iPhone 12 Pro specifications](https://support.apple.com/en-us/111875)

In MuJoCo 4.0.1, three repeated open–close sweeps per fixed-base scene reached both command limits.
The projected distance between the opposing pad meshes ranged from 1.4 to
110.7 mm. Abrupt full-range commands produced up to 3.28 mm of transient
loop separation, which settled below 0.02 mm. In a separate fixture, the same
gripper in each configuration held a 40 mm, 60 g cube for 2 s with bilateral
contact after its support was removed. At a 1 rad/s command rate, the peak loop separation was
0.176 mm. The cube released onto the floor on command. All runs completed
without simulator warnings.

## Source and license

The 18 STL meshes match the published MagiClaw model assets byte for byte. The
linkage and actuator settings come from the ASimpleMagic fixed-base workbench.
The original BSD 3-Clause notice is included
with the model. [Pinned model source](https://github.com/asMagiClaw/magiclaw-model/tree/c71dbb9a5ab853d32190a52089064dc31c647f65) · [License](LICENSE)

See [CHANGELOG.md](CHANGELOG.md).
