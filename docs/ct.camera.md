# ct.camera <badge>new in v1.3</badge>

::: tip Hey,
This page describes the methods and parameters of `ct.camera` object in a form of a reference. You can learn about techniques and usage in a more free form at the ["Working with Viewport" page](/viewport-management.html).
:::

## Camera's Geometry

### `ct.camera.x`, `ct.camera.y`

The real x and y coordinates of the camera. It does not have a screen shake effect applied, as well as may differ from `targetX` and `targetY` if the camera is in transition.

### `ct.camera.targetX` and `ct.camera.targetY`

The x and y coordinates of the target location. Moving it instead of just using the `x`/`y` parameter will trigger the drift effect.

### `ct.camera.computedX`, `ct.camera.computedY`

The resulting position of the camera in game coordinates. These have screen shake and `ct.camera.shiftX`, `ct.camera.shiftY` applied.

### `ct.camera.width`, `ct.camera.height`

The width and height of the camera of the unscaled shown region. Use `ct.camera.scale` to get a scaled version. To change these value, see `ct.width` and `ct.height` properties.

### `ct.camera.rotation`

A value in degrees that rotate the camera.

### `ct.camera.scale.x`, `ct.camera.scale.y`

A scalar value that scales the capturing rectangle. If compared to image viewing tools, `1` and `1` means no scaling, `0.5` will zoom in to a 200% view, `3` will zoom out and produce 33% scaling.

### `ct.camera.left`, `ct.camera.top`, `ct.camera.right` and `ct.camera.bottom`

These represent the resulting location of a particular side of the camera in game units. Those cannot be changed manually.

### `ct.camera.uiToGameCoord(x, y)` and `ct.camera.gameToUiCoord(x, y)`

Convert a point from one coordinate space to another. These return an array with two elements: x and y coordinates.

There are also `ct.u.uiToGameCoord` and `ct.u.gameToUiCoord`, that call these methods of the current `ct.camera` object.

### `ct.camera.getTopLeftCorner()`, `ct.camera.getTopRightCorner()`, `ct.camera.getBottomLeftCorner()`, `ct.camera.getBottomRightCorner()`

Return an array with two elements, x and y coordinates. These are in game coordinates, and take rotation and scaling into account.

### `ct.camera.getBoundingBox()`

Returns a bounding box of the camera, in game coordinates. See [PIXI.Rectangle](https://pixijs.download/release/docs/PIXI.Rectangle.html) for its properties.

## Following a Copy

### `ct.camera.follow`

If set, the camera will follow the given copy.

### `ct.camera.followX`, `ct.camera.followY`

Works if `follow` is set to a copy. Setting one of these to `false` will disable automatic camera in a given direction.

### `ct.camera.borderX`, `ct.camera.borderY`

Works if `follow` is set to a copy. Sets the frame inside which the copy will be kept, in game pixels. Can be set to `null` so the copy is set to the center of the screen.

## Screen Shake and Wobble

### `ct.camera.shake`

The current power of a screen shake effect, relative to the screen's max side (100 is 100% of screen shake). If set to 0 or less, it, disables the effect.

### `ct.camera.shakePhase`

The current phase of screen shake oscillation.

### `ct.camera.shakeDecay`

The amount of `shake` units substracted in a second. Default is 5.

### `ct.camera.shakeFrequency`

The base frequency of the screen shake effect. Default is 50.

### `ct.camera.shakeX`, `ct.camera.shakeY`

A multiplier applied to the screen shake effect. Default is 1.

### `ct.camera.shakeMax`

The maximum possible value for the `shake` property to protect players from losing their monitor, in `shake` units. Default is 10.

## Other

### `ct.camera.drift`

If set to a value between 0 and 1, it will make camera movement smoother

### `ct.camera.shiftX`, `ct.camera.shiftY`

These displace the camera in UI units, but do not change `ct.camera.x` or `ct.camera.y`.

### `ct.camera.realign(room)`

Realigns all the copies in a room based on new dimensions of a camera. This is useful for quick positioning of UI elements on different screens. You can skip the realignment for some copies if you set their `skipRealign` parameter to `true`.

### `ct.camera.manageStage()`

This will align all non-UI layers in the game according to the camera's transforms. This is automatically called internally, and you will hardly ever use it.

## Spawning a new instance of a camera

You can create a new camera object for your needs by calling a `Camera` constructor:

```js
const oldCamera = ct.camera;
ct.camera = new Camera(0, 0, 1024, 768);
```