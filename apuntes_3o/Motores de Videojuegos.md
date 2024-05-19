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



___
Model review diferencias, para que se suelen utilizar
Meshes euler
Meshes summary of mesh representation operaciones
Tessellation ordenes de los algoritmos
Forward diferences
Algoritmo de teselacion 
Simplification operaciones, basados en 
Theoreum
Modelos discretos y continuos
Progresive meshes