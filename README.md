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

### 7. use coroutine instead of update to do simple animations 

Actually, consider using a tween library such as DOTween, iTween, etc.

### 8. use event to simplify dependency

think about events as a "broadcasting" system

### 9. stick to coding conventions

参考[C# Style Guide](https://github.com/raywenderlich/c-sharp-style-guide#fields--variables)

关于变量名camelcase的问题，个人偏好public和property用大写Camelcase，private用小写Camelcase。

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



## Editor

### 1. use icons to organize your scene



## Project Management



## TODO(could use some help:)

1. Add more code examples
2. Add more tips on various topics
3. Add more links to useful resources