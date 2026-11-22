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

## Compatibility

Both variants were tested in native MuJoCo 4.0.0 and 4.0.1. Set the contact
solver options at the scene level when combining robots. The supplied scenes use an elliptic friction cone,
`impratio="10"`, and `noslip_iterations="1"`.

## Source and citation

This package uses the MJCF and 18 visual and collision meshes from the
[pinned Newton asset revision](https://github.com/newton-physics/newton-assets/tree/f8fb7abcbeba2318814a74f3eeb02780ad7925d6/asroballet).
The Menagerie layout keeps the original mesh bytes and physics parameters.
The [Newton package README](https://github.com/newton-physics/newton-assets/blob/f8fb7abcbeba2318814a74f3eeb02780ad7925d6/asroballet/README.md)
links the structured USD assets and ONNX policies.

The MJCF and meshes are released under the [MIT License](LICENSE). Cite the
[asRoBallet paper](https://arxiv.org/abs/2604.24916) when using the model in research.

See [CHANGELOG.md](CHANGELOG.md).
