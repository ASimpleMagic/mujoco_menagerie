# asMagiClaw (MJCF)

asMagiClaw is a motor-driven two-finger gripper developed by the Design and
Learning Research Group. This package models the on-robot gripper mechanism
with the original shell, flange, four-bar linkages, and rigid fingertip
contacts. [MagiClaw project and paper](https://arxiv.org/abs/2509.19169)

## Open and close the gripper

Open `scene.xml` in MuJoCo. The fixed-base workbench provides `home` and
`open` reset keyframes. In **Controls**, set `claw_beam` to `1.10` rad to
open the fingers or `-0.02` rad to close them. Adjust the target gradually
for smooth motion.

Use `asmagiclaw.xml` to attach the gripper to a robot. In the authored
model frame, +X points toward the fingers and +Z points up. `ft_frame` is the
original shell-origin reference, and `grasp_reference` is a nominal point
0.30 m forward of that origin.

## Model and validation

Six hinge coordinates describe the linkages. A joint equality synchronizes the
two driven beams, and two point equalities close the follower loops. The
mechanism has one independent motion. The position actuator is bounded to
±3 N·m. Mass and inertia use the Studio workbench's CAD-derived PLA estimates.
The contact model treats the MetaFinger surfaces as rigid.

In MuJoCo 4.0.1, three repeated open–close sweeps reached both command limits.
The projected distance between the opposing pad meshes ranged from 1.4 to
110.7 mm. Abrupt full-range commands produced up to 3.28 mm of transient
loop separation, which settled below 0.02 mm. In a separate fixture, the same
gripper held a 40 mm, 60 g cube for 2 s with bilateral contact after its
support was removed. At a 1 rad/s command rate, the peak loop separation was
0.176 mm. The cube released onto the floor on command. All runs completed
without simulator warnings.

## Source and license

The 12 STL meshes match the published on-robot model assets byte for byte.
The linkage and actuator settings come from the ASimpleMagic fixed-base
workbench. The assembly uses the bare on-robot shell and flange.
The original BSD 3-Clause notice is included
with the model. [Pinned model source](https://github.com/asMagiClaw/magiclaw-model/tree/c71dbb9a5ab853d32190a52089064dc31c647f65) · [License](LICENSE)

See [CHANGELOG.md](CHANGELOG.md).
