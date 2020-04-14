# ansel
A plug and play `Virtual Camera`
This repository was spun off from [Claude](https://github.com/bb-labs/claude) as a standalone npm module. It's completely dependency free and thus can be dropped right into any graphics application.

```sh
npm install ansel
```

It's straightforward enough to use, given coordinates in raster space (apologies for the jargon) we might first convert them to screen space:

```js
rasterToScreen(x, y) {
    /** Convert Raster-Space Coordinates to Screen-Space */
    return [
        2 * x / this.canvas.width - 1,
        1 - 2 * y / this.canvas.height,
    ]
}

const [x, y] = rasterToScreen(100,100)
```

We can cast rays (unit vectors from our viewpoint):

```js
const ray = this.camera.cast(x, y)
```

Or perform viewing transforms:

```js
this.camera.zoom(event.deltaY)

this.camera.to = new Float32Array([1,7,1])
this.camera.from = new Float32Array([1,0,0])

this.camera.view()
```

We keep the state in the camera class for efficient updates. It gets expensive to new up arrays with each transform call. And that's pretty much it. We can now look around 3D space!



