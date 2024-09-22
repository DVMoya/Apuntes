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

## STEERING BEHAVIORS

This discussion of specific steering behaviors assumes that locomotion is implemented by the
simple vehicle model described above, and is parameterized by a single steering force vector.

### Seek

**Seek** acts to steer the character towards a specified position in global space. The *desired velocity* is a vector in the direction from the character to the target. The length of *desired velocity* could be *max_speed*, or it could be the characters current speed, depending on the particular application. The steering vector is the difference between this desired velocity and the character's current velocity, see Figure 3.

![[seek.png|400]]

```cpp
desired_velocity = normalize(position - target) * max_speed
steering = desired_velocity - velocity
```

### Flee

**Flee** is simply the inverse of **seek** and acts to steer the character so that its velocity is radially aligned away from the target. The desired velocity points in the opposite direction.

### Pursuit

**Pursuit** is similar to **seek** except that the quarry (target) is another moving character. Effective pursuit requires a prediction of the target's future position. Steering for **pursuit** is then simply the result of applying the **seek** steering behavior to the predicted target location. See Figure 4.

![[pursuit&evasion.png|400]]

### Evasion

**Evasion** is analogous to **pursuit**, except that **flee** is used to steer away from the predicted future position of the target character. 

### Offset Pursuit

**Offset pursuit** refers to steering a path which passes near, but not directly into a moving target. The basic idea is to dynamically compute a target point which is offset by a given radius R from the predicted future position of the quarry, and to then use **seek** behavior to approach that offset point, see Figure 5.

![[offsetPursuit.png|400]]

### Arrival

**Arrival** behavior is identical to **seek** while the character is far from its target. But instead of moving through the target at full speed, this behavior causes the character to slow down as it approaches the target, eventually slowing to a stop coincident with the target, as shown in Figure 6.

![[arrival.png|400]]

```cpp
target_offset = target - position
distance = length(target_offset)
ramped_speed = max_speed * (distance / slowing_distance)
clipped_speed = minimum(ramped_speed, max_speed)
desired_velocity = (clipped_speed / distance) * target_offset
steering = desired_velocity - velocity
```

### Obstacle Avoidance

**Obstacle avoidance** behavior gives a character the ability to maneuver in a cluttered environment by dodging around obstacles.

The goal of the behavior is to keep an imaginary cylinder of free space in front of the character. The cylinder lies along the character's forward axis, has a diameter equal to the character's bounding sphere, and extends from the character's center for a distance based on the character's speed and agility. An obstacle further than this distance away is not an immediate threat.

The **obstacle avoidance** behavior considers each obstacle in turn (perhaps using a spatial portioning scheme to cull out distance obstacles) and determines if they intersect with the cylinder. The local obstacle center is projected onto the side-up plane (by setting its forward coordinate to zero) if the 2D distance from that point to the local origin is greater than the sum of the radii of the obstacle and the character, then there is no potential collision. Remaining obstacles a line-sphere intersection calculation is performed. The obstacle which intersects the forward axis nearest the character is selected as the *most threatening.*

Steering to avoid this obstacle is computed by negating the (lateral) side-up projection of the obstacle's center. In Figure 7 obstacle A does not intersect the cylinder, obstacles B and C do, B is selected for avoidance, and corrective steering is to the character's left.

![[obstacleAvoidance.png|400]]

The value returned from obstacle avoidance is either:
**(A)** The steering value to avoid the most threatening obstacle.
**(B)** If no collision is imminent, a special value (a null value, or the zero vector) to indicate that no corrective steering is required at this moment.

### Wander

Wander is a type of random steering. One easy implementation would be to generate a random steering force each frame, but this produces rather uninteresting motion. It is *twitchy* and produces no sustained turns. A more interesting approach is to retain steering direction state and make small random displacements to it each frame. Thus at one frame the character may be turning up and to the right, and on the next frame will still be turning in almost the same direction.

This idea can be implemented several ways, but one that has produced good results is to constrain the steering force to the surface of a sphere located slightly ahead of the character. To produce the steering force for the next frame: a random displacement is added to the previous value, and the sum is constrained again to the sphere's surface. The sphere's
radius (the large circle in Figure 8) determines the maximum wandering *strength* and the magnitude of the random displacement (the small
circle in Figure 8) determines the wander *rate.*

![[wander.png|400]]

Related to **wander** is **explore** (where the goal is to exhaustively cover a region of space) and **forage** (combining wandering with resource seeking).

### Path Following

**Path following** behavior enables a character to steer along a predetermined path, such as a roadway, corridor or tunnel. **Path following** behavior is intended to produce motion such as people moving down a corridor.

To compute steering for **path following**, a velocity-based prediction is made of the character's future position, as discussed above in regard to
obstacle avoidance behavior. The predicted future position is projected onto the nearest point on the path spine. See Figure 9.

![[pathFollowing.png|400]]

To steer back towards the path, the **seek** behavior is used to steer towards the on-path projection of the predicted future position.

Variations on **path following** include **wall following** and **containment** as shown in Figure 10.

![[wallFollowing&containment.png|400]]

**Wall following** means to approach a *wall* and then to maintain certain offset from it. **Containment** refers to motion which is restricted to remain within a certain region.

### Flow Field Following

**Flow field following** steering behavior provides a useful tool for directing the motion of characters based on their position within an environment. In **flow field following** behavior the character steers to align its motion with the local tangent of a *flow field.* The flow field defines a mapping from a location in space to a flow vector: imagine for example a floor with arrows painted on it.

The implementation of flow field following is very simple. The future position of a character is estimated and the flow field is sampled at that location. This flow direction (vector F in Figure 11) is the *desired velocity* and the steering direction (vector S) is simply the difference between the current velocity (vector V) and the desired velocity.

![[flowFollowing.png|400]]

### Unaligned Collision Avoidance

**Unaligned collision avoidance** behavior tries to keep characters which are moving in arbitrary directions from running into each other.

To implement this as a steering behavior, our character considers each of the other characters and determines (based on current velocities) when and where the two will make their nearest approach. It will steer laterally to turn away from the potential collision. It will also accelerate forward or
decelerate backwards to get to the indicate site before or after the predicted collision. In Figure 12 the character approaching from the right decides to slow down and turn to the left, while the other character will speed up and turn to the left.

![[unalignedCollisionAvoidance.png|400]]

### The Neighborhood

The next three steering behaviors: **separation**, **cohesion**, and **alignment**, relate to groups of characters. In each case, the steering behavior determines how a character reacts to other characters in its local neighborhood. Characters outside of the local neighborhood are ignored. As shown in Figure 13, the neighborhood is specified by a distance which defines when two characters are *nearby*, and an angle which defines the character's perceptual *field of view.*

![[neighborhood.png|400]]

### Separation

**Separation** steering behavior gives a character the ability to maintain a certain separation distance from others nearby. To compute steering for separation, first a search is made to find other characters within the specified neighborhood. For each nearby character, a repulsive force is computed by subtracting the positions of our character and the nearby
character, normalizing, and then applying a $1/r$ weighting. (That is, the position offset vector is scaled by $1/r^2$ .) Note that $1/r$ is just a setting that has worked well, not a fundamental value. These repulsive forces for each nearby character are summed together to produce the overall steering force. See Figure 14.

![[separation.png|400]]

### Cohesion

**Cohesion** steering behavior gives an character the ability to cohere with (approach and form a group with) other nearby characters. See Figure 15.

![[cohesion.png|400]]

Steering for **cohesion** can be computed by finding all characters in the local neighborhood (as described above for separation), computing the *average position* (or *center of gravity*) of the nearby characters. The steering force can applied in the direction of that *average position* or it can be used as the target for **seek** steering behavior.

### Alignment

**Alignment** steering behavior gives an character the ability to align itself with other nearby characters, as shown in Figure 16.

![[alignment.png|400]]

Steering for **alignment** can be computed by finding all characters in the local neighborhood (as described above for **separation**), averaging together the velocity (or alternately, the unit forward vector) of the nearby characters. This average is the *desired velocity,* and so the
steering vector is the difference between the average and our character's current velocity (or alternately, its unit forward vector). This steering
will tend to turn our character so it is aligned with its neighbors.

### Flocking

**Flocking behavior**: in addition to other applications, the **separation**, **cohesion** and **alignment** behaviors can be combined to produce the *boids model* of flocks, herds and schools. In some applications it is sufficient to simply sum up the three steering force vectors to produce a single combined steering for flocking (see **Combining Behaviors** below). However for better control it is helpful to first normalize the three steering components, and then to scale them by three weighting factors before summing them. As a result, *boid flocking* behavior is specified by nine numerical parameters: a *weight* (for combining), a *distance* and an *angle* (to define the neighborhood, see Figure 13) for each of the three component behaviors.

### Leader Following

**Leader following** behavior causes one or more character to follow another moving character designated as the leader. The implementation of leader following relies on **arrival** behavior (see above) a desire to move towards a point, slowing as it draws near. See Figure 17.

![[leaderFollowing.png|400]]

### Combining Behaviors

Combining behaviors can happen in two ways. A character may sequentially switch between behavioral modes as circumstances change in its world. These discrete changes of behavioral state take place at the *action selection level.*

On the other hand, some kinds of behaviors are commonly blended together, effectively acting in parallel. This behavioral blending occurs at the middle steering level of the behavioral hierarchy.

Blending of steering behaviors can be accomplished in several ways. The most straightforward is simply to compute each of the component steering behaviors and sum them together, possibly with a weighting factor for each of them. it is not the most computationally efficient approach, and despite adjusting the weights, component behaviors may cancel each other out at inopportune times.

The computation load can be decreased by observing that a character's momentum serves to apply a low-pass filter to changes in steering force.

The problem of components canceling each other out can be addressed by assigning a priority to components. The steering controller first checks to see if obstacle avoidance returns a non-zero value (indicating a potential collision), if so it uses that. Otherwise, it moves on to the second priority behavior, and so on.