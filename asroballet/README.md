# asRoBallet (MJCF)

asRoBallet is an underactuated humanoid ballbot with three omni-wheel drive motors
and an actuated upper body.

## Scene variants

| Scene | Ball configuration |
| --- | --- |
| [`scene.xml`](scene.xml) | Default. An independent free joint lets contact couple the ball to the wheels and floor. This is the default configuration in the [Newton v1.6.0 example](https://github.com/newton-physics/newton/blob/v1.6.0/newton/examples/robot/example_robot_asroballet.py). |
| [`scene_ball_joint.xml`](scene_ball_joint.xml) | A spherical joint connects the ball to the base and lets it rotate around the joint anchor. |

The standalone robot entries are
[`asRoBallet_floating_ball.xml`](asRoBallet_floating_ball.xml) and
[`asRoBallet.xml`](asRoBallet.xml). Load `scene.xml` in MuJoCo Studio to open the default scene.
Balancing and tracking require a controller.

### Upright reset

The floating-ball scene provides an `upright` keyframe. It resets the base and
ball to their initial poses with zero velocity, holds both elbows at π/2 rad
to match the arms-down controller pose, and sets wheel commands to zero.

```python
import mujoco

model = mujoco.MjModel.from_xml_path("asroballet/scene.xml")
data = mujoco.MjData(model)
mujoco.mj_resetDataKeyframe(model, data, model.key("upright").id)
mujoco.mj_forward(model, data)
```

## Compatibility

Both variants were tested in native MuJoCo 4.0.0 and 4.0.1. Set the contact
solver options at the scene level when combining robots. The supplied scenes use an elliptic friction cone,
`impratio="10"`, and `noslip_iterations="1"`.

### Closed-loop validation

The default floating-ball scene was exercised in native MuJoCo 4.0.1 from
`upright` on Apple Silicon. The test used the published station-keeping and
velocity-tracking ONNX policies at 100 Hz, with the observation and action
mapping from the [Newton v1.6.0 example](https://github.com/newton-physics/newton/blob/v1.6.0/newton/examples/robot/example_robot_asroballet.py).

- Station keeping for 20 s had 0.090 m maximum displacement from the starting
  position of `slam_site` and 0.67° maximum absolute roll or pitch.
- Four 10 s tracking trials covered forward, lateral, yaw, and combined
  commands. Across the trials, the largest per-axis mean absolute error after
  2 s was 0.082 m/s for planar velocity and 0.037 rad/s for yaw rate. Maximum
  absolute roll or pitch was 2.20° or less.
- Three repeats of each trial produced identical sampled states and controls
  on that host. Every sampled floor contact in the controlled trials was on
  the ball.

## Source and citation

This package uses the MJCF and 18 visual and collision meshes from the
[pinned Newton asset revision](https://github.com/newton-physics/newton-assets/tree/f8fb7abcbeba2318814a74f3eeb02780ad7925d6/asroballet).
The Menagerie layout keeps the original mesh bytes and physics parameters.
The [Newton package README](https://github.com/newton-physics/newton-assets/blob/f8fb7abcbeba2318814a74f3eeb02780ad7925d6/asroballet/README.md)
links the structured USD assets and ONNX policies.

The MJCF and meshes are released under the [MIT License](LICENSE). Cite the
[asRoBallet paper](https://arxiv.org/abs/2604.24916) when using the model in research.

See [CHANGELOG.md](CHANGELOG.md).
