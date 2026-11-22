# asOverDog (MJCF)

asOverDog is a quadruped with three variants of its closed-chain leg mechanism.

| Variant | Scene | Robot model |
| --- | --- | --- |
| Bennett (default) | [scene.xml](scene.xml) | [asoverdog_bennett.xml](asoverdog_bennett.xml) |
| Planar | [scene_planar.xml](scene_planar.xml) | [asoverdog_planar.xml](asoverdog_planar.xml) |
| Spherical | [scene_spherical.xml](scene_spherical.xml) | [asoverdog_spherical.xml](asoverdog_spherical.xml) |

Open the complete `asoverdog` folder in ASimpleMagic Studio. Under **Entry model**,
choose a scene and click **Apply**. The model starts in its `home` keyframe
with the source's 0.34 m base height, then settles onto the floor. Set the
actuator inputs to zero to hold the published home joint angles. Each input is
a position offset in radians from that angle, limited to ±0.35 rad and ±17 N·m.
Choose **home** under **Keyframe** to reset and repeat the test. [ASimpleMagic Studio](https://asimplemagic.com/)

## Conversion

The MJCF preserves the source body's mass properties, joint names and axes,
joint limits, motor armature and damping, and the CAD mesh geometry. Four
pairs of point constraints close the four revolute loops. Each pair constrains
the hinge pivot and a second point along its axis, leaving rotation about the
axis free. The 20 tree hinge coordinates have 12 independent leg degrees
of freedom with the loops active.

The Planar variant enables non-adjacent self-collisions. Bennett and Spherical
follow their source profiles with self-collisions disabled. MuJoCo uses the
convex hulls of the Spherical variant's collision meshes.

The included position servos support interactive testing and small joint
commands. The published Newton gait policies use a separate observation and
learned-actuator pipeline that would need a MuJoCo adapter.

## Validation

All three scenes were tested in MuJoCo 4.0.1. Each 10 s run started at
`home`, settled on the floor, then exercised the four front thigh and calf
servos with position offsets up to 0.07 rad. There were three runs per
variant with identical sampled-state hashes for each variant, no warnings,
and floor contacts confined to the feet. Peak loop-anchor separation stayed
below 0.44 mm in every run, including touchdown.

The home pose was compared with the same revision's Newton 1.5.1 CPU reset.
Body origins agreed within 1 µm and orientations within 0.001°. All three
scenes also loaded and ran in the public ASimpleMagic Studio editor with
zero simulator warnings or errors.

## Source and license

Meshes were converted to STL and the robot, floor scene, and actuator setup
were adapted to MJCF for ASimpleMagic. The original assets are from the
[asOverDog Newton source at `1944bea`](https://github.com/asOverDog/asoverdog_newton/tree/1944bea98439215e2ba64c969fb345c0e4c92d02).
The model and mesh assets are distributed under the [Apache License 2.0](LICENSE).

See [CHANGELOG.md](CHANGELOG.md).
