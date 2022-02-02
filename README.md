# FreeMatrix Utility For Unity

For developers recently starting out with Unity, it might be hard to convert between the world unit, local unit and pixels due to the fact the local units scale based on the parent object's scale. Simple primitive animations such as pointing to a direction and scaling up or scaling down an object through code might also be hard for some peope. 

This is where FreeMatrix Utility For Unity comes into play. 

## Features

### The utility has three (3) main classes as of the moment 
#### 1. Time
Coding timers in Unity is simple, developers usually multiply a rate by UnityEngine's Time.deltaTime, however, often times it might be too repetitive and the developers have less control on sudden timer changes.

In FreeMatrix Utility, a developer could create multiple independent timers that have types. You could even control the scale of each individual timers and decide what type of timer would it be. 

Here is an example (supposed you were to create a countdown timer that goes faster overtime
Instead of: 
```C#
float timeMax = 30;
float currentTime = 30;
float scale = 1;
 
void Update()
{
  if(currentTime <= 0)
  {
      currentTime = timeMax;
      scale++;
  }

  currentTime -= scale * Time.deltaTime;
 }
```

You'll be using: 
```C#
FreeMatrix.Utility.Time time = new FreeMatrix.Utility.Time(FreeMatrix.Utility.Time.TYPE.COUNTDOWN, 30, 1);

void Update()
{ 
  if(time.Update())
  {
     time.scale++; // Property field
  }
}
```

#### 2. Convert2D
Unity uses a system of measurement called "units" which are by default 100pixels each. While this is easy to use, this creates a problem when one wants to convert between local units (scaled by parents), world units (unity default) and pixels, confusing newer developers and prompting them to almost use calculators all the time. 

FreeMatrix makes it easier in a way to convert between the value between the three much simpler and much easier. 

For Example (Suppose you want to check the current scale of a child object in world units)
```C#
GameObject gameObject = GameObject.Find("Test");
// We will be using Vector2 here as the current class is for 2D
Vector2 scaleInUnit = FreeMatrix.Utility.Convert2D.LocalToPixel(gameObject.transform.parent.gameObject.localScale, gameObject.transform.localScale);
scaleInUnit = FreeMatrix.Utility.Convert2D.PixelToWorld(scaleInUnit);

Debug.Log(scaleInUnit);
```

#### 3. Tween2D
Usually, basic primitive animations like increasing/decreasing a game object's scale over a set period of time is confusing for newer developers. Pointing to a direction might be hard for some as well given that it involves angles. 

FreeMatrix Utility makes it simpler and easier 

For Example (Supposed you were to point to a target)

```C#
// The object would immediately point to the target
gameObject.transform.localRotation = Quaternion.Euler(FreeMatrix.Utility.Tween2D.PointTo(destination, gameObject.transform.localPosition, gameObject.transform.localRotation));
```
