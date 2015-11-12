# Unity Tanks Tutorial
## Concepts Learned
===================================================================================================
# Index
1. [Scene Setup](#01-scene-setup)
2. [Tank Creation & Control](#02-tank-creation--control)
3. [Camera Control](#03-camera-control)
4. [Tank Control](#04-tank-health)
5. [Shell Creation](#05-shell-creation)
6. [Firing Shells](#06-firing-shells)
7. [Game Managers](#07-game-managers)
8. [Audio Mixing](#08-audio-mixing)

===================================================================================================

### 01. [Scene Setup](http://unity3d.com/learn/tutorials/projects/tanks-tutorial/scene-setup?playlist=20081)
***Basic scene setup***

#### General
* Dragging models into scene or hierarchy
* Frame selecting: dbl-click GameObject, or 'F' key in scene

#### Lighting
* Dedicated window for lighting options
* Precomputed Real Time GI
    * Baking (bg process)
    * Low resolution OK for lowpoly models
* Ambient light source & color vs. skybox
 
===================================================================================================

### 02. [Tank Creation & Control](http://unity3d.com/learn/tutorials/projects/tanks-tutorial/tank-creation-control?playlist=20081)
***How to add the tank artwork and components to let the player control the tank.***

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
   *  Colliders (primitive)
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
   * Blue vs gray text in Hierarchy: Saved vs. unsaved changes to prefabs from scene gameobjects
		* Also ***bold*** fields in Inspector are unsaved changes to prefabs

#### Particle Systems
* World vs. Local simulation space
* Simulate over time vs. distance
* Various options for behavior

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
* Quaternion representation in Unity for rotations of Transformations
   *  Quaternion.Euler() method for easy Euler angle conversions

===================================================================================================

### 03. [Camera Control] (http://unity3d.com/learn/tutorials/projects/tanks-tutorial/scene-setup?playlist=20081)
***How to create a Camera rig which pans and zooms to keep all tanks on-screen at once.***

* Creation of an empty GameObject called CameraRig to house a Script Component: CameraControl.cs
* Rig becomes parent of the existing MainCamera
* Scripted to keep both tanks in view: Pan and Zoom (i.e. move & resize frustum)
	* Tanks will stay in camera's frustum: area b/w near & far clip plane
	* Perspective frustum: variable size clip planes
	* Orthographic frustum: same size clip planes, hence no change in scale over distance
	* Orthographic Camera size in relation to aspect ratio (16:9) & aspect (1.77).
* GameObject.GetComponentInChildren<ComponentType>() method OK if child component type is unique.
* [HideInInspector] attribute to prevent public member from being serialized to Inspector.

===================================================================================================

### 04. [Tank Health](http://unity3d.com/learn/tutorials/projects/tanks-tutorial/tank-health?playlist=20081)
***Setup tank damage, update UI heal slider based on health value, tank deactivation on death***

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

===================================================================================================

### 05. [Shell Creation](http://unity3d.com/learn/tutorials/projects/tanks-tutorial/shell-creation?playlist=20081)
***Create a ballistic shell for the tank & a radius for explosion forces***

* Collider triggers for simply creating callbacks in scripts to react to, instead of physical forces.
* Physics.OverlapSphere(pos,radius,layer) method to get an array of colliders touching/inside a specified sphere.
* Rigidbody.AddExplosionForce(force,pos,radius) to simulate explosive forces.
* Component references can also be used to get other component references on same GameObject via GetComponent<>().

===================================================================================================

### 06. [Firing Shells](http://unity3d.com/learn/tutorials/projects/tanks-tutorial/firing-shells?playlist=20081)
***How to fire projectiles, and make a UI & sound effect to accompany the mechanic.***

* Re-appropriate a UI Slider to make an aiming guide.
* Shells are unoptimally instantiated and destroyed every fire. Object pooling pattern would solve this.

===================================================================================================

### 07. [Game Managers](http://unity3d.com/learn/tutorials/projects/tanks-tutorial/game-managers?playlist=20081)
***Game loop architecture using coroutines and textual UI creation for messaging players.***

* Text UI GameObject creation and usage, along with Shadow script component for effect.
* [Serializable] attribute on classes are serialized for view in the Inspector.
* ColorUtility.ToHtmlStringRGB(Color) for converting an rgb color to HTML code for rich text.
* Coroutine are used to cleverly manage the main game loop.

#### Coroutines
* A function that can suspend its execution (yield) until the given `YieldInstruction` finishes.
* Normal coroutine updates are run after the *Update()* function returns.
* Can be used as a way to spread an effect over a period time
* It is also a **useful optimization** since it also allows you to determine at what rate any function gets called.

**Return types & different uses of Coroutines:**

```csharp
yield                       // The coroutine will continue after all Update functions have been called on the next frame.
yield WaitForSeconds        // Continue after a specified time delay, after all Update functions have been called for the frame
yield WaitForFixedUpdate    // Continue after all FixedUpdate has been called on all scripts
yield WaitForEndOfFrame     // Continue after all FixedUpdate has been called on all scripts
yield WWW                   // Continue after a WWW download has completed.
yield StartCoroutine        // Chains the coroutine, and will wait for the MyFunc coroutine to complete first.
```

**Coroutines also admit a nice, slick, readable game loop:**

```csharp
void Start() {
    // ... other start code ...
    StartCoroutine (GameLoop()); // Let's play!
}

// This is called from start and will run each phase of the game one after another.
private IEnumerator GameLoop() {
    yield return StartCoroutine (LevelStart()); // Start the level: Initialize, do some fun GUI stuff, ..., WaitForSeconds if setup too fast.
    yield return StartCoroutine (LevelPlay());  // Let the user(s) play the level until a win or game over condition is met, then return back here.
    yield return StartCoroutine (LevelEnd());   // Find out if some user(s) "won" the level or not. Also, do some cleanup.
    
    if (WinCondition) { // Check if game level progression conditions were met.
        Application.LoadLevel(++level); // or Application.LoadLevel(Application.loadedLevel) if using same scene
    } else { // Let the user retry the level by restarting this (non-yielding) coroutine again.
        StartCoroutine (GameLoop());
    }
}
```

===================================================================================================

### 08. [Audio Mixing](http://unity3d.com/learn/tutorials/projects/tanks-tutorial/audio-mixing?playlist=20081)
***Balance the audio in the game with a dynamic mix where sound effects duck the volume of the music.***

* A MainMix audio mixer default is created that outputs directly to the AudioListener.
* Audio Mixer window is used to create 3 additional Audio Mixer Groups: Music, SFX, Driving.
	* Used to modify/mix the audio output before reaching the AudioListener.
* Audio Source components (in our Prefabs) are setup to output their clips through the Audio Mixer Groups.
	* Default setup was to output clips straight to the AudioListener, without mixing.
* A "Duck Volume" effect is then used to lower the bg music when sfx are playing.
	* The SFX group is setup to "Send Effect" its signal to the Music group's "Duck Volume" effect.

===================================================================================================