# Unity Tanks Tutorial
## Concepts Learned

===================================================================================================

### 01. Scene Setup
#### General
* Dragging models into scene or hierarchy
* Frame selecting: dbl click GO, 'F' key in scene

#### Lighting
* Dedicated window for options
* Precomputed Real Time GI
    * Baking (bg process)
    * Low resolution for lowpoly models
* Ambient light source & color vs. skybox
 
===================================================================================================

### 02. Tank Creation & Control
#### General
* Layers
   * For collider interaction isolation
   * Only collider owner needs to be on layer (parent GO, not children)
* Duplication of GameObjects (Ctrl+D or right-click context menu)
* Project Settings
   * Input Manager: configuring input control & names

#### Components
* Component adding, setup, & collapsing
   *  Rigidbody
      * req'd for Physics system
      * constraints on axes (position/rotation)
      * Kinematics: turn on/off (receive physical forces/no forces)
   *  Colliders (primitve)
      * reports physics events (collisions) to Rigidbody
      * Trigger vs. Physical events
      * proper sizing for model
   * Audio Source
      * Populating references using "Circle Select" in Inspector
         * versus dragging from Project Assets folders
      * Empty references to be populated at runtime via scripting
   * Scripts
      * are also Components (provided they extend from Monobehaviour)

#### Prefabs      
* Dragging configured scene objects from Hierarchy into Project Prefabs folder
   * and vice versa
* Prefab options: Select, Revert, Apply 
   * between prefab & scene object linkage
   * Applying changes from changed Hierarchy/Scene game objects to prefabs.

#### Particle Systems
* World vs. Local simulation space
* Simulate over time vs. distance
* Various options for behaviour

#### Scripting
* Script editing, compiling, serializing workflow in Unity
* Console window messages for debugging.
* Public vs. Private fields/member variables
   * relation to Inspector view (public fields show up for editing & populating references)
   * UnassignedReferenceExceptions when forgetting to assign reference in Inspector panel.
* Inspector serialized values override values assigned in the script's public/serializable variables.
* Dynamically referencing & manipulating Components at runtime
* Variable naming conventions
   * e.g. m_Name denotes class member variable (scoping mnemonic)
* TankMovement (inherits from MonoBehavior)
   * Script Component for Tank GameObject to control its movement
   * coding MonoBehaviour Event methods (Awake, Start, Update, etc)
* Vector manipulation math for Rigidbody movement by applying forces via method calls
* Quaternion represenatation in Unity for rotations of Transformations
   *  Quaternion.Euler() method for easy euler angle conversions

===================================================================================================

### 03. Camera Control
