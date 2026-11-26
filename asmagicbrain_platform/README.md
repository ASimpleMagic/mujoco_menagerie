# asMagicBrain Platform (MJCF)

The asMagicBrain Platform is a modular workbench for the Embodied AI Systems
course. The four scenes share a 500 × 540 mm optical plate, mounting frames,
asBrain Box enclosure and a rear-mounted laptop. The editable platform geometry
follows the reference dimensions and frame placement of the course's robot
viewer. Fixtures, perforations and laptop details are simplified for simulation.

## Configurations

| Configuration | MJCF entry | Joints / controls | Studio |
| --- | --- | ---: | --- |
| Platform | [scene.xml](scene.xml) | 0 / 0 | [Open in Studio](https://asimplemagic.com/?sample=asmagicbrain-platform) |
| Platform + reBot Arm | [scene_rebot.xml](scene_rebot.xml) | 8 / 7 | [Open in Studio](https://asimplemagic.com/?sample=asmagicbrain-rebot) |
| Standalone LEAP Hand | [scene_leap.xml](scene_leap.xml) | 16 / 16 | [Open in Studio](https://asimplemagic.com/?sample=asmagicbrain-leap) |
| reBot Arm + wrist-mounted LEAP Hand | [scene_rebot_leap.xml](scene_rebot_leap.xml) | 22 / 22 | [Open in Studio](https://asimplemagic.com/?sample=asmagicbrain-rebot-leap) |

Studio opens each scene paused in the main editor. The arm starts at the
course viewer's home pose. Its parallel gripper has two coupled slides and one
control. The mounted right LEAP Hand replaces the parallel gripper and uses
the viewer's thumb-up wrist adapter. Arm joint controls 2, 3 and 4 are radian
offsets from home. The controls for the LEAP fingers are absolute joint angles.
Select **Run** in the simulator and expand **Inspector → Controls** to
explore the joints. **Reset** returns to home. The fixtures and motion are
for simulation.

## Source and license

- **Workbench and fixtures.** ASimpleMagic's editable MJCF for the course
  platform, including the mounting plates, simplified enclosure and generic
  laptop. The platform frame uses +X right, +Y rear and +Z up, in metres.
  The workbench and original fixture definitions use Apache-2.0.
- **reBot Arm B601-RS.** The native [Class 08 model](https://github.com/asEmbodiedAISyst/2026Autumn/tree/c88cb573c8e8429a54d16a008fb3dd5ff4f5e437/2026-autumn/resources/class08/additional_material/model/rebot_b601_rs_mjcf)
  derives from Seeed Studio's [RS mechanical description](https://github.com/Seeed-Projects/reBot-DevArm/tree/c247ea9cb0da29cd52c31953659cc8c47e6d1a6e/Rebot_Arm_description/RS).
  Seeed Studio Co., Ltd. © 2026. The supplied URDF and mesh sources are
  in [assets/rebot](assets/rebot). The reBot model and source assets use
  CERN-OHL-W-2.0. ASimpleMagic's 2026-11-27 adaptation places the arm on
  the platform, sets the home joint references and gripper travel, and
  replaces the gripper with a wrist fixture in the combined scene.
- **Right LEAP Hand.** The [Menagerie right hand](https://github.com/ASimpleMagic/mujoco_menagerie/tree/17a358c3bdc49e3e2ce2785ced5b6ca5c400acfa/leap_hand)
  by Ananye Agarwal, copyright 2023, uses MIT. The scene assembly gives its
  elements unique names, sets the standalone and wrist mounting transforms,
  and adds gravity compensation for each finger.

The component terms and notices are in [LICENSE](LICENSE). Cite Kenneth Shaw,
Ananye Agarwal and Deepak Pathak, *LEAP Hand: Low-Cost, Efficient, and
Anthropomorphic Hand for Robot Learning*, Robotics: Science and Systems, 2023,
when using the hand.
