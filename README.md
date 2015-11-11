# Unity Tanks Tutorial
## Concepts Learned

===================================================================================================

### 01. [Scene Setup](http://unity3d.com/learn/tutorials/projects/tanks-tutorial/scene-setup?playlist=20081)
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

### 02. [Tank Creation & Control](http://unity3d.com/learn/tutorials/projects/tanks-tutorial/tank-creation-control?playlist=20081)
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
   * Blue vs grey text in Hierarchy: Saved vs. unsaved changes to prefabs from scene gameobjects
		* Also ***bold*** fields in Inspector are unsaved chages to prefabs

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

### 03. [Camera Control] (http://unity3d.com/learn/tutorials/projects/tanks-tutorial/scene-setup?playlist=20081)
* Creation of an empty GameObject called CameraRig (which will contain a Script Component: CameraControl.cs)
	* New parent of the existing MainCamera
* Scripted to keep both tanks in view: Pan and Zoom (resize frustrum)
	* Tanks will stay in camera's frustum (area b/w near & far clip plane)
	* Perspective frustrum: variable size clip planes
	* Orthographic frustum: same size clip planes, hence no change in scale over distance
	* Orthographic Camera size in relation to aspect ratio (16:9) & aspect (1.77).
* GameObject.GetComponentInChildren<ComponentType>() method OK if child component type is unique.
* [HideInInspector] attribute to prevent public member from being serialized to Inspector.


### 04. [Tank Health](http://unity3d.com/learn/tutorials/projects/tanks-tutorial/tank-health?playlist=20081)
* ***Setup tank damage, update UI heal slider based on health value, tank deactivation on death***
* Using a Unity UI Slider as a radial health bar.
* UI Elements: Canvas, Slider, EventSystem
* EventSystem Input Module component in Inspector
    * Axis setup along with InputManager
* Canvas Scaler (Script) component for helping developing multiresolution apps
* Canvas component Render modes: Screenspace vs. Worldspace
* Rect Transform component in all UI elements.
* Anchor presets button to edit anchors (Shift/Alt)
* Top to Bottom rendering of UI child elements of Canvas (as found in the Hierarchy)
* Instantiating inactive game objects (e.g. particle systems) to cache them until ready for use.
	* Also, setting them inactive again instead of destroying them then reinstantiating again.
	* Caching like this (inactive->active) saves on garbage collection calls.