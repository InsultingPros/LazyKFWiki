# A collection of edits for my user configs

Sources:

- [Steam: Mouse Lag Fix](https://steamcommunity.com/sharedfiles/filedetails/?id=910000377)
- [TWI: Precaching settings](https://forums.tripwireinteractive.com/index.php?threads/to-decrease-loadtimes-turn-off-precaching-and-change-game-cache-size.38730/#post-855070)
- [Steam: Additional tweaks](https://steamcommunity.com/sharedfiles/filedetails/?id=329586515)

## KillingFloor.ini

### Better 3D Sound

```java
[ALAudio.ALAudioSubsystem]
UseEAX=True
Use3DSound=True
UseDefaultDriver=False
CompatibilityMode=False
MaxEAXVersion=255
ReverseStereo=False
// higher values can change the sound a lot
Channels=64
```

### FPS / Lag fixes

Default settings trigger lots of hitches and lags during gameplay. Let's fix it.

This loads the longest, but is the most stable.

```java
UsePrecaching=True
bNeverPrecache=True
UsePreCache=False
```

This one has x2 quicker load times.

```java
UsePrecaching=False
bNeverPrecache=True
UsePreCache=True
```

```java
[Engine.GameEngine]
// anything above 256 will crash the game eventually
CacheSizeMegs=256


[Engine.Engine]
// your gpu vram size
DetectedVideoMemory=2048
// unlocks higher quality AA methods if you have nvidia
NVidiaGPU=True


[D3D9Drv.D3D9RenderDevice]
// additional vars for higher stability
CheckForOverflow=True
AvoidHitches=True
```

### Part #2 for fixing mouse smoothing

> Changing the minimum desired framerate ensures that framerate smoothing is not activated, which negatively affects mouse input. Setting Reduce Mouse Lag to false ensures that it remains off. 

```java
[SDLDrv.SDLClient]
[WinDrv.WindowsClient]
MinDesiredFrameRate=1.000000


// depending on what renderer you use
[D3DDrv.D3DRenderDevice]
[D3D9Drv.D3D9RenderDevice]
[OpenGLDrv.OpenGLRenderDevice]
[PixoDrv.PixoRenderDevice]
ReduceMouseLag=False
```

## User.ini

### Part #1 for fixing mouse smoothing

Mouse smoothing is a pure cancer in this game. Don't forget to check Killingfloor.ini edits as well. 

```java
[Engine.Input]
// by default its 2.0
MouseX=Count bXAxis | Axis aMouseX Speed=1.0
MouseY=Count bYAxis | Axis aMouseY Speed=1.0


[Engine.PlayerInput]
MouseSmoothingMode=0
MouseSmoothingStrength=0.000000
MouseSamplingTime=0.001000
// this resets every time you check ingame menu
MouseAccelThreshold=-1
// i started to use 6000 DPI D:
MouseSensitivity=0.500000


// better change for all these ctrl's
[XInterface.GUIController]
[GUI2K4.UT2K4GUIController]
[KFGui.KFGUIController]
MenuMouseSens=0.400000
```

### Disable auto switch on weapon pickup

We do not want to auto switch to picked up weapon. NEVER!

```java
[Engine.PlayerController]
bNeverSwitchOnPickup=True
```

### Remove Pawn Blur Effect

```java
[KFmod.KFHumanPawn]
// true is the default
bUseBlurEffect=False
```
