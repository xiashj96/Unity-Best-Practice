# Unity-Best-Practice
Some useful tips that I find useful while learning Unity.

Disclaimer: These tips are not absolute. Some of them might be actually bad in some situations, in light of the fact that I am still struggling to learn unity right now.

## Scripting

###  1. use attribute to attach additional behavior to the methods and variables you create

```c#
public class SpinScript : MonoBehaviour 
{
    [Range(-100, 100)] public int speed = 0;

    void Update () 
    {
        transform.Rotate(new Vector3(0, speed * Time.deltaTime, 0));
    }
}
```

```c#
[ExecuteInEditMode]
public class ColorScript : MonoBehaviour 
{
    void Start()
    {
        renderer.sharedMaterial.color = Color.red;
    }
}
```

```c#
[HideInInspector] public bool inMainMenu;
```

[Attribute Refernce](http://docs.unity3d.com/412/Documentation/ScriptReference/20_class_hierarchy.Attributes.html)

### 2. use properties instead of simple public variables in monobehaviour script 

### 3. do not use only monobehaviour

### 4. use static, monobehavior, scriptableobject and singleton according to the situation

ScriptableObject:

```c#
using UnityEngine;

[CreateAssetMenu]
public class MyScriptableObject : ScriptableObject 
{
	public int SomeVariable;
  	
    void OnEnable() {
  	
	}
    void OnDisable() {
  	
	}
    void OnDestroy() {
  	
	}
}
```

```c#
ScriptableObject.CreateInstance<MyScriptableObject>();
```

Application:

- data tables
- ...

### 5. keep in mind some general coding principles

- SINGLE RESPONSIBILITY: A given class should be, ideally, responsible for just one task.
- ABSTRACTION: see next rule
- MODULARIZATION

### 6. use interface to abstract game object functionality

eg: IDamageable, IInventory

### 7. use coroutine instead of update to do simple routines 

Also consider Invoke() and InvokeRepeating() .

Actually, consider using a tween library such as DOTween, iTween, etc.

### 8. use event to simplify dependency

think about events as a "broadcasting" system

### 9. stick to coding conventions

参考[C# Style Guide](https://github.com/raywenderlich/c-sharp-style-guide#fields--variables)

关于变量名大小写的问题，个人偏好public和property用小写Camelcase，private用下划线小写Camelcase，因为这样与	Unity本身的命名是一致的。

### 10. really know what Monobehaviour does

[Monobehaviour Reference](http://docs.unity3d.com/Manual/ExecutionOrder.html)

1. use Awake() to set up references and Begin() to initialize
2. sometimes it's useful to implement some non-monobehaviour functions to be called by other scripts

### 11. robustness

```c#
if (hit.Rigidbody != null) {
  doSomthing();
}
else {
  Debug.Log("No Rigidbody attached to " + hit.name);
}
```

### 12. implement reset() for scripts that are reused extensively in your game

### 13. increase script reusability by separating data and logic

eg: Health.cs, Attack.cs

Data should only be assigned to public variables. Implementations should not contain any specific data.

### 14. use finite state machine to organize your game or a particular game object

A simple and nice implementation here: [Unity3d-Finite-State-Machine](https://github.com/thefuntastic/Unity3d-Finite-State-Machine)

### 15. disable and enable components in a game object to achieve flexible behaviour 

### 16. prefer event to SendMessage()

SendMessage(), BroadcastMessage() and SendMessageUpwards() use reflection and are therefore expensive. More importantly, they can result in ugly code and unexpectable errors.

### 17. use UnityEvent instead of plain C#  event# 

UnityEvent is similar to C# delegate and event, but is also compatible with UI system.

### 18. Prefer GameObject.FindWithTag() to GameObject.Find()

The latter use string matching and is therefore more expensive.

### 19. Think in terms of event-driven programming, don't just put everything in Update()

example:

```C#
public class EnemyObject : MonoBehaviour
{
//-------------------------------------------------------
//C# accessors for private variables
public int Health
{
  get{return _health;}
  set
  {
    //Clamp health between 0-100
    _health = Mathf.Clamp(value, 0, 100);
    //Check if dead
    if(_health <= 0)
    {
      OnDead();
      return;
    }
    //Check health and raise event if required
    if(_health <= 20)
    {
      OnHealthLow();
      return;
    }
  }
}
//-------------------------------------------------------
public int Ammo
{
  get{return _ammo;}
  set
  {
    //Clamp ammo between 0-50
    _ammo = Mathf.Clamp(value,0,50);
      //Check if ammo empty
    if(_ammo <= 0)
    {
      //Call expired event
      OnAmmoExpired();
      return;
    }
  }
}
```

### 20. Remove unused MonoBehaviour methods()

Empty monobehaviour methods will still be called if not removed.

### 21. Make every public fields properties and serialize private fields to make them editable in the inspector. 

This is for the sake of encapsulation.

## Editor

### 1. use icons to organize your scene



## Animation

### 1. consider adjusting the curve in key frame animation

### 2. consider using IK(Inverse Kinematics) for Humanoid characters with a avatar 

### 3. precompute hash values for animator parameters

because us string directly in Update() can be computationally expensive

```c#
using UnityEngine;
using System.Collections;

public class EthanScript : MonoBehaviour 
{
    Animator anim;
    int jumpHash = Animator.StringToHash("Jump");
    int runStateHash = Animator.StringToHash("Base Layer.Run");


    void Start ()
    {
        anim = GetComponent<Animator>();
    }


    void Update ()
    {
        float move = Input.GetAxis ("Vertical");
        anim.SetFloat("Speed", move);

        AnimatorStateInfo stateInfo = anim.GetCurrentAnimatorStateInfo(0);
        if(Input.GetKeyDown(KeyCode.Space) && stateInfo.nameHash == runStateHash)
        {
            anim.SetTrigger (jumpHash);
        }
    }
}
```

### 4. use root motion if you want animation to control the gameobject's position

### 5. use animation events to set up effects that are closely related to animation

e.g: foot step sound in walk/jump animation

## Audio

### 1. use audio mixer snapshot and exposed parameter to control audio in script



## Physics

### 1. motion must be relative to time





## Generic

### 1. break large projects down into smaller, more manageable pieces 

### 2. make prefabs such that it will just work when you drag it into the scene 

### 3. code duplication is a warning sign that you should refactor your code

### 4. code iteratively

Premature optimization is evil!








## TODO(could use some help:)

1. Add more code examples
2. Add more tips on various topics
3. Add more links to useful resources