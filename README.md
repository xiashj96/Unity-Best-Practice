# Unity-Best-Practice
Some useful tips that I find useful while learning Unity.

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

### 7. use coroutine instead of update 

### 8. use event to simplify dependency

think about events as a "broadcasting" system

### 9. stick to coding conventions

参考[C# Style Guide](https://github.com/raywenderlich/c-sharp-style-guide#fields--variables)

关于变量名camelcase的问题，个人偏好public和property用大写Camelcase，private用小写Camelcase。

### 10. really know what Monobehaviour does

[Monobehaviour Reference](http://docs.unity3d.com/Manual/ExecutionOrder.html)

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

## Editor

### 1. use icons to organize your scene



## More...