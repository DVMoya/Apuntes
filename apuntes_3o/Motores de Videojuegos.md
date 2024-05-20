___
# INDEX
___

- [[#CHAPTER 1 GAME ENGINE ARCHITECTURE]]
	- [[#WHAT KIND OF GAMES?]]
	- [[#GAME ENGINE]]
	- [[#WHY DO DIFFERENT GAME ENGINES RUN AT DIFFERENT FPS?]]
	- [[#GAME ENGINE LAYERS]]
	- [[#TOOLS AND THE ASSET PIPELINE]]
	- [[#GAME LOOP]]
- [[#CHAPTER 2 GEOMETRIC MODELING]]
	- [[#MODEL REVIEW]]
	- [[#MESHES]]
	- [[#TESSELLATION]]
	- [[#SIMPLIFICATION]]
	- [[#LEVEL OF DETAIL (MULTIRESOLUTION MODEL)]]
- [[#CHAPTER 3 SCENE REPRESENTATION]]
	- [[#WHY DO WE NEED NEW TECHNIQUES?]]
	- [[#SCENE GRAPHS]]
	- [[#SPACE PARTITIONING]]
	- [[#VISIBILITY DETERMINATION *(CULLING)*]]
- [[#CHAPTER 4 VISUAL REALISM]]

___
# CHAPTER 1 : GAME ENGINE ARCHITECTURE
___

## WHAT KIND OF GAMES?

- **Computer simulation.** Mathematical model (approximation & simplification)
- **Agent-based.** Interactive entities.
- **Interactive real-time simulation.** The game world is dynamic.
- **"Soft" real-time system.** The deadlines are not catastrophic.

The games work in the same way than numerical simulations, running a *"game loop".*

![[game_loop.png|500]]

In contrast to its mathematical model:

![[math_game_loop.png|500]]

##  GAME ENGINE

Software that is extensible and can be used as the foundation for many different games without major modification.

## WHY DO DIFFERENT GAME ENGINES RUN AT DIFFERENT FPS?

Because each engine has it own needs regarding simulation speed. For example:

- Render. 1/24 second (30 – 60 fps)
- Physics. 1/120 second 
- IA. 1 times per second 
- Audio. 1/60 second

## GAME ENGINE LAYERS

Game engines are built in layers:

- Target Driver
- Device Driver
- Operating System
- *Third-Party SDKs and Middleware*
- *Platform Independence Layer*
- *Core System*
- *Resource Manager*
- *Rendering Engine*
- *Profiling and Debugging Tools*
- *Collision and Physics*
- *Animation*
- *Human Interface Devices*
- *Audio*
- *Online Multiplayer / Networking*
- *Gameplay Foundation Systems*
- *Game Specific Subsystems*

![[gm_layers_1.png|500]]![[gm_layers_2.png|500]]![[gm_layers_3.png|500]]

## TOOLS AND THE ASSET PIPELINE

### Digital Content Creation Tools

![[digital_content_creation_tools.png|500]]

### The Asset Conditioning Pipeline

The data formats are rarely suitable for direct use in-game (too much information too slow to read).

- **3D Model/Mesh Data**
	- Brush geometry (edited in the game world editor)
	- 3D Models (Meshes)
		- Mesh: Triangles or quads, with different materials
		- Model: Composite object with multiple meshes, animation data and other metadata (COLLADA)
- **Skeletal Animation Data**
- **Audio Data**
	- Mono, stereo, 5.1, 7.1
	- Wave files (.wav) are common
	- PlayStation ADPCM (.vag)
- **Particle System Data**
	- There are third-party tools, such as Houdini, that allows film-quality effects.
	- Some engines have their own system.

### The World Editor

- **Radiant** → Quake
- **Hammer** → Half-Life 2
- **UnrealEd** → Unreal Engine
- **Unity 3D**

## GAME LOOP

### The Rendering Loop

The entire contents of the screen change continuously.

![[rendering_loop.png|500]]

### The Game Loop

A game is composed of many different subsystems.

![[game_loop_loop.png|500]]

### Unity 3D

![[unity_1.png|500]]![[unity_2.png|500]]

___
# CHAPTER 2 : GEOMETRIC MODELING
___

## MODEL REVIEW

![[model_review.png|500]]

## MESHES

### Euler-Poincaré formula

Let the number of vertices be *V*, edges be *E*, bodies be *B*, and let the genus be *G.* Then, to denote a meaningful geometric object, the mesh must satisfy the generalized formula:

$$
	F - E + V - L = 2(B - G)
$$

### Mesh representations

- Vertex-vertex meshes:

![[vertex_vertex_meshes.png|300]]

- Face-vertex meshes

![[face_vertex_meshes.png|300]]

- Winged-edged meshes

![[winged_edged_meshes.png|300]]

![[summary_mesh_representation.png|500]]

## TESSELLATION

### Algorithm Concave **$O(n^3)$**

1. Examine each segment joining two vertices.
2. If the segment intersects with other segment, it can not be used.
3. Else the returning polygon is divided and the process is repeated with the two parts.

![[algorithm_concave.png|200]]

With more complex algorithms it can reach *$O(n).$*

### Ear Clipping **$O(n^2)$**

1. find all the triangles with vertices (i, i+1, i+2) and detect whether the segment (i, i+2) cuts any polygon edge.
2. Remove all triangles found and recalculate if it is necessary.

![[ear_clipping.png|400]]

More complex methods can work in *$O(n·log(n))$.*

### Forward differencing

- Fast evaluation of polygonal functions in uniform intervals.
- Numerical problems. All values are calculated with additions.
- Ideal for future implementations HW (Moreton).

![[forward_differencing.png|400]]

### Tessellation algorithm

**Adaptive.** The edges are subdivided taking into account the curvature, the length of the edges or the pixel size.

![[tessellation_algorithm.png|400]]

**Problem.** Holes between different Levels of subdivision.

## SIMPLIFICATION

- Main characteristic of these algorithms.
	- Speed (no real-time)
	- Quality of the exportation (in some sense)
	- Managing different kinds of input meshes.
- Classification
	- Simplification operation
	- Simplification metric (geometric-based or image-based)

### Simplification operation

- Vertex-clustering

![[vertex_clustering.png|400]]

- Vertex removal

![[vertex_removal.png|400]]

- Edge collapse

![[edge_collapse.png|400]]

- Contraction of pairs of vertices

![[contraction_vertices.png|400]]

### Metrics

- Geometric

![[simplification_geometric.png|400]]

- Image-based

![[image_based_simplification.png|400]]

## LEVEL OF DETAIL (MULTIRESOLUTION MODEL)

### **Discrete models**

*Features:*

- Each mesh can be obtained by simplification.
- Each mesh is associated with a range of LODs.
- There are a limited number of meshes.
- Standard technology in UNITY and other engines.

*Disadvantages:*

- Each mesh is stored independently.
- It is difficult to adapt the LOD to the application.
- Popping.
- Uniform resolution.

*Solutions:*

- Morphing.
- Blending.

![[discrete_models.png|300]]

### **Continuous models**

*Features:*

- Efficient extraction of LOD in real-time.
- Adequate size (2 to 3 times the original model).
- Continuous meshes.
- Smooth transition between levels.

*Classification:*

- Uniform domain

![[uniform_domain.png|400]]

- variable domain

![[variable_domain.png|400]]

### Tree-based models

- Quadtrees.

![[quadtree.png|400]]

- Restricted quadtrees

![[restriced_quadtree.png|400]]

- Bintrees

![[bintrees.png|400]]

___
# CHAPTER 3 : SCENE REPRESENTATION
___

## WHY DO WE NEED NEW TECHNIQUES?

Because we need to increase efficiency. *Clipping* and *Z-buffer* have a linear cost with the number of primitives.

## SCENE GRAPHS

- **Node:** element of a scene graph.
	- *Groups:* nodes with children.
	- *Leaves:* nodes without children.
- **Components of a node:** set of attributes.
	- Geometry.
	- Color.
	- Sound.
	- A component can be referenced by more than one object.

![[scene_graph.png|500]]

## SPACE PARTITIONING

Process of dividing a space into non-overlapping regions. Space-partitioning systems are often hierarchical (Tree).

*Features:*
- The acceleration of the visibility computation.
	- Send only the visible triangles from the point of view.
	- Removing a big amount of polygons (no per triangle).

*Types:*
- **BSP** (Binary Space Partition) **Trees.**
- **Octrees.**

### BSP Trees

*Types:*
- Aligned with the axis.
- Aligned with polygons.

*Main idea:*
- Divide the space with a plane.
- Locate geometry in space to which it belongs.
- Apply the process recursively.

#### Aligned with the *axis*

![[aligned_with_axis_1.png|400]]![[aligned_with_axis_2.png|400]]![[aligned_with_axis_3.png|400]]

#### Aligned with *polygons*

![[aligned_with_polygons_1.png|400]]![[aligned_with_polygons_2.png|400]]

### Octrees

![[octrees_1.png|400]]![[octrees_2_example.png|400]]

*Algorithm features:*
- **Subdivision**
	- Until the boxes have a number of triangles.
	- Until some subdivision level is reached.
	- Until a number of boxes is reached on the tree.
- **When the triangles intersect several boxes**
	- Place the triangles in the larger cube containing it.
	- Divide the triangle.
	- Place the triangle in both boxes.
- **Use**
	- Combination with skeleton of visible polygons (Hierarchical Frustum Culling).

## VISIBILITY DETERMINATION *(CULLING)*

***Culling*. Select from a group for reject.**
- Usually happens before Visible Surface Determination in a rendering pipeline.
- Primitives or batches of primitives can be rejected in their entirety (reducing the load).
- Objects that are invisible do not have to be fetched, transformed, rasterized or shaded.
- *Types:*
	- Back-face culling.
	- Hierarchical view-frustum culling.
	- Detail culling.
	- Occlusion culling (Portal culling).

![[culling_techniques.png|500]]

This requires way more explanation for each culling method, but I'm lazy so... Tough luck finding anything else in here.

___
# CHAPTER 4 : VISUAL REALISM
___



___
Tema 4
Soft shadows (PCSS)
Hay 4 Algoritmos 4 preguntas xd
Shadow volumen