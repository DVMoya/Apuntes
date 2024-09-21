___
# STEERING BEHAVIAORS FOR AUTONOMOUS CHARACTERS (paper by Craig W. Reynolds)
___

## INTRODUCTION

![[hierarchyOfMotionBehaviors.png|400]]

The category of situated, embodied agents usually suggests  autonomous robots: mechanical devices that exist in the real world.

*Behavior:* can mean complex action of a human or other animal based on volition or instinct. It can also mean largely predictable actions of a simple mechanical system, or the complex action of a chaotic system.

## LOCOMOTION

*Locomotion* is the bottom of the three level behavioral hierarchy. It converts control signals from the steering layer into motion of the character's *body.*

The locomotion of an autonomous character can be based on, or independent from, its animated portrayal. A hybrid approach is to use a simple locomotion model and an adaptive animation model, like an inverse-kinematics driven walk cycle, to bridge the gap between abstract locomotion and concrete terrain.

## A SIMPLE VEHICLE MODEL

This vehicle model is based on a point mass approximation. A point mass is defined by a *position* property and a *mass* property. In addition, the simple vehicle model includes a *velocity* property. The velocity is modified by applying forces. These forces are generally self-applied, and hence limited. For the simple vehicle model, this notion is summarized by a single *maximum force* parameter (max_force). As an alternative to realistic simulation of all the limiting forces, the simple vehicle model includes a *maximum speed* parameter (max_speed). Finally, the simple vehicle model also includes an *orientation* parameter.

```
Simple Vehicle Model:
	mass        scalar
	position    vector
	velocity    vector
	max_force   scalar
	max_speed   scalar
	orientation N basis vectors
```

For a 3D vehicle model, the position and velocity vector values have three components and the *orientation* value is a set of three vectors (or a 3x3 matrix, or a quaternion). For a 2D vehicle, the vectors each have two components, and the *orientation* value is two 2D basis vectors or can be represented as a single scalar heading angle.

The physics of the simple vehicle model is based on forward Euler integration.

``` cpp
steering_force = truncate(steering_direction, max_force)
acceleration = steering_force/mass
velocity = truncate(velocity + acceleration, max_speed)
position = position + velocity
```

The local coordinate system is defined in terms of four vectors: a position vector specifying the local origin, and three direction vectors serving as the basis vectors of the space. These axes will be referred to here as *forward*, *up*, and *side*.

In order to remain aligned with velocity at each time step, the basis vectors must be rotated into a new direction.

```cpp
new_forward = normalize(velocity)
approximate_up = normalize(approximate_up)
new_side = cross(new_forward, approximate_up)
new_up = cross(new_forward, new_side)
```

For a *surface hugging* (wheeled, sliding, or legged) vehicle, we want to both constrain the vehicle's position to the surface and to align the vehicle's *up* axis to the surface normal. In addition the velocity should be constrained to be purely tangential to the surface. These requirements can be easily met if the surface manifold is represented in such a way that an arbitrary point in space can be mapped to:

1. The nearest point to the surface.
2. The surface normal at that point.

The vehicle's position is set to the point on the surface, ans the surface normal becomes its *up* axis.

Because of its assumption of velocity alignment, this simple vehicle model cannot simulate effects such as skids, spins or slides. Furthermore this model allows the vehicle to turn when its speed is zero. It allows undesirably large changes in orientation during a single time step. This problem can be solved by placing an additional constraint on change of orientation, or by limiting the lateral steering component at low speeds, or by simulating moment of inertia.