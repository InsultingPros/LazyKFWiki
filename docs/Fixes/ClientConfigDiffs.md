!> In case of a fuckup you can wipe your configs and restore them from "..\Your KF Dir\System\": [Default.ini](https://github.com/InsultingPros/LazyKFWiki/releases/download/1.0.0/Default.ini) and [defuser.ini](https://github.com/InsultingPros/LazyKFWiki/releases/download/1.0.0/defuser.ini).

A collection of edits for my user configs.

## **KillingFloor.ini**

### Better 3D Sound

```js
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

```js
UsePrecaching=True
bNeverPrecache=True
UsePreCache=False
```

This one has x2 quicker load times.

```js
UsePrecaching=False
bNeverPrecache=True
UsePreCache=True
```

```js
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

### Part #1 for fixing mouse smoothing

> Changing the minimum desired framerate ensures that framerate smoothing is not activated, which negatively affects mouse input. Setting Reduce Mouse Lag to false ensures that it remains off.

```js
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

## **User.ini**

### Part #2 for fixing mouse smoothing

Mouse smoothing is a pure cancer in this game. Don't forget to check Killingfloor.ini edits as well.

```js
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

```js
[Engine.PlayerController]
bNeverSwitchOnPickup=True
```

### Remove Pawn Blur Effect

```js
[KFmod.KFHumanPawn]
// true is the default
bUseBlurEffect=False
```

## **Sources**

- [Steam: Mouse Lag Fix](https://steamcommunity.com/sharedfiles/filedetails/?id=910000377)
- [TWI: Precaching settings](https://forums.tripwireinteractive.com/index.php?threads/to-decrease-loadtimes-turn-off-precaching-and-change-game-cache-size.38730/#post-855070)
- [Steam: Additional tweaks](https://steamcommunity.com/sharedfiles/filedetails/?id=329586515)
