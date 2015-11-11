# Unity Tanks Tutorial
## Concepts Learned

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
   * and vive versa
* Prefab options: Select, Revert, Apply 
   * between prefab & scene object linkage

#### Particle Systems
* World vs. Local simulation space
* Simulate over time vs. distance
* Various options for behaviour

#### Scripting
* TankMovement (inherits from MonoBehavior)
   * Script Component for Tank GameObject to control its movement
   * MonoBehaviour Event methods
* Variable naming conventions
   * e.g. m_Name denotes class member variable (scoping mnemonic)
* Public vs. Private fields/member variables
   * relation to Inspector view
*

