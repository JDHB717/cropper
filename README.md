# [Cropper](https://github.com/fengyuanchen/cropper)

> A simple jQuery image cropping plugin.

- [Demo](http://fengyuanchen.github.io/cropper)
- [Cropper without jQuery](http://github.com/fengyuanchen/cropperjs)



## Features

- Supports [options](#options)
- Supports [methods](#methods)
- Supports [events](#events)
- Supports touch (mobile)
- Supports zoom
- Supports rotation
- Supports scale (flip)
- Supports canvas
- Supports multiple croppers
- Supports to crop image in the browser-side with canvas
- Cross-browser support



## Main

```
dist/
├── cropper.css     ( 5 KB)
├── cropper.min.css ( 4 KB)
├── cropper.js      (70 KB)
└── cropper.min.js  (25 KB)
```



## Getting started

### Quick start

Four quick start options are available:

- [Download the latest release](https://github.com/fengyuanchen/cropper/archive/master.zip).
- Clone the repository: `git clone https://github.com/fengyuanchen/cropper.git`.
- Install with [NPM](http://npmjs.org): `npm install cropper`.
- Install with [Bower](http://bower.io): `bower install cropper`.



### Installation

Include files:

```html
<script src="/path/to/jquery.js"></script><!-- jQuery is required -->
<link  href="/path/to/cropper.css" rel="stylesheet">
<script src="/path/to/cropper.js"></script>
```

#### [CDNJS](https://cdnjs.com/)

The CDNJS provides CDN support for Cropper's CSS and JavaScript. You can find the links [here](https://cdnjs.com/libraries/cropper).


#### [RawGit](https://rawgit.com/)

```html
<link  href="https://cdn.rawgit.com/fengyuanchen/cropper/v1.0.0/dist/cropper.min.css" rel="stylesheet">
<script src="https://cdn.rawgit.com/fengyuanchen/cropper/v1.0.0/dist/cropper.min.js"></script>
```


### Usage

Initialize with `$.fn.cropper` method.

```html
<!-- Wrap the image or canvas element with a block element -->
<div class="container">
  <img src="picture.jpg">
</div>
```

```js
$('.container > img').cropper({
  aspectRatio: 16 / 9,
  crop: function(e) {
    // Output the result data for cropping image.
    console.log(e.x);
    console.log(e.y);
    console.log(e.width);
    console.log(e.height);
    console.log(e.rotate);
    console.log(e.scaleX);
    console.log(e.scaleY);
  }
});
```

#### FAQ

See the [FAQ](FAQ.md) documentation.


#### Notes

- The size of the cropper inherits from the size of the image's parent element (wrapper), so be sure to wrap the image with a visible block element.

- The outputted cropped data bases on the original image size, so you can use them to crop the image directly.

- If you try to start cropper on a cross-origin image, please make sure that your browser supports HTML5 [CORS settings attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/CORS_settings_attributes), and your image server supports the `Access-Control-Allow-Origin` option.


#### Known issues

- About `getCroppedCanvas` method: The `canvas.drawImage` API in some Mac OS / iOS browsers will rotate an image with EXIF Orientation automatically, so the output cropped canvas may be incorrect. To fix this, you may upload the cropped data and crop the image in the server-side, see the example: [Crop Avatar](examples/crop-avatar). Or you may handle the EXIF Orientation with canvas as [JavaScript Load Image](https://github.com/blueimp/JavaScript-Load-Image) or in server as PHP first before to use cropper.

- [Known iOS resource limits](https://developer.apple.com/library/mac/documentation/AppleApplications/Reference/SafariWebContent/CreatingContentforSafarioniPhone/CreatingContentforSafarioniPhone.html): As iOS devices limit memory, the browser may crash when you are cropping a large image (iPhone camera resolution). To avoid this, you may resize the image first (below 1024px) before start a cropper.



## Options

You may set cropper options with `$().cropper(options)`.
If you want to change the global default options, You may use `$.fn.cropper.setDefaults(options)`.


### viewMode

- Type: `Number`
- Default: `0`
- Options:
  - `0`: the crop box is just within the container
  - `1`: the crop box should be within the canvas
  - `2`: the canvas should not be within the container
  - `3`: the container should be within the canvas

Define the view mode of the cropper.


### aspectRatio

- Type: `Number`
- Default: `NaN`

Set the aspect ratio of the crop box. By default, the crop box is free ratio.


### data

- Type: `Object`
- Default: `null`

The previous cropped data if you had stored, will be passed to `setData` method automatically.


### preview

- Type: `String` (**jQuery selector**)
- Default: `''`

Add extra elements (containers) for previewing.

**Notes:**

- The maximum width is the initial width of preview container.
- The maximum height is the initial height of preview container.
- If you set an `aspectRatio` option, be sure to set the preview container with the same aspect ratio.
- If preview is not getting properly displayed, set `overflow:hidden` to the preview container.


### responsive

- Type: `Boolean`
- Default: `true`

Rebuild the cropper when resize the window.


### checkImageOrigin

- Type: `Boolean`
- Default: `true`

By default, the plugin will check the image origin, and if it is a cross-origin image, a `crossOrigin` attribute will be added to the image element and a timestamp will be added to the image url to reload the image for "getCroppedCanvas".

By adding `crossOrigin` attribute to image will stop adding timestamp to image url, and stop reload of image.


### modal

- Type: `Boolean`
- Default: `true`

Show the black modal above the image and under the crop box.


### guides

- Type: `Boolean`
- Default: `true`

Show the dashed lines above the crop box.


### center

- Type: `Boolean`
- Default: `true`

Show the center indicator above the crop box.


### highlight

- Type: `Boolean`
- Default: `true`

Show the white modal above the crop box (highlight the crop box).


### background

- Type: `Boolean`
- Default: `true`

Show the grid background of the container.


### autoCrop

- Type: `Boolean`
- Default: `true`

Enable to crop the image automatically when initialize.


### autoCropArea

- Type: `Number`
- Default: `0.8` (80% of the image)

A number between 0 and 1. Define the automatic cropping area size (percentage).


### dragCrop

- Type: `Boolean`
- Default: `true`

Enable to remove the current crop box and create a new one by dragging over the image.


### movable

- Type: `Boolean`
- Default: `true`

Enable to move the image.


### rotatable

- Type: `Boolean`
- Default: `true`

Enable to rotate the image.


### scalable

- Type: `Boolean`
- Default: `true`

Enable to scale the image.


### zoomable

- Type: `Boolean`
- Default: `true`

Enable to zoom the image.


### mouseWheelZoom

- Type: `Boolean`
- Default: `true`

Enable to zoom the image by wheeling mouse.


### wheelZoomRatio

- Type: `Number`
- Default: `0.1`

Define zoom ratio when zoom the image by wheeling mouse.


### touchDragZoom

- Type: `Boolean`
- Default: `true`

Enable to zoom the image by dragging touch.


### cropBoxMovable

- Type: `Boolean`
- Default: `true`

Enable to move the crop box.


### cropBoxResizable

- Type: `Boolean`
- Default: `true`

Enable to resize the crop box.


### doubleClickToggle

- Type: `Boolean`
- Default: `true`

Enable to toggle drag mode between "crop" and "move" when double click on the cropper.


### minContainerWidth

- Type: `Number`
- Default: `200`

The minimum width of the container.


### minContainerHeight

- Type: `Number`
- Default: `100`

The minimum height of the container.


### minCanvasWidth

- Type: `Number`
- Default: `0`

The minimum width of the canvas (image wrapper).


### minCanvasHeight

- Type: `Number`
- Default: `0`

The minimum height of the canvas (image wrapper).


### minCropBoxWidth

- Type: `Number`
- Default: `0`

The minimum width of the crop box.


### minCropBoxHeight

- Type: `Number`
- Default: `0`

The minimum height of the crop box.


### build

- Type: `Function`
- Default: `null`

A shortcut of the "build.cropper" event.


### built

- Type: `Function`
- Default: `null`

A shortcut of the "built.cropper" event.


### cropstart

- Type: `Function`
- Default: `null`

A shortcut of the "cropstart.cropper" event.


### cropmove

- Type: `Function`
- Default: `null`

A shortcut of the "cropmove.cropper" event.


### cropend

- Type: `Function`
- Default: `null`

A shortcut of the "cropend.cropper" event.


### crop

- Type: `Function`
- Default: `null`

A shortcut of the "crop.cropper" event.


### zoom

- Type: `Function`
- Default: `null`

A shortcut of the "zoom.cropper" event.



## Methods

As there is an **asynchronous** process when load the image, you **should call most of the methods after built**, except "setAspectRatio", "replace" and "destroy".

```js
$().cropper({
  built: function () {
    $().cropper('method', argument1, , argument2, ..., argumentN);
  }
});
```


### crop()

Show the crop box manually.

```js
$().cropper({
  autoCrop: false,
  built: function () {
    // Do something here
    // ...

    // And then
    $(this).cropper('crop');
  }
});
```


### reset()

Reset the image and crop box to their initial states.


### clear()

Clear the crop box.


### replace(url)

- **url**:
  - Type: `String`
  - A new image url.

Replace the image's src and rebuild the cropper.


### enable()

Enable (unfreeze) the cropper.


### disable()

Disable (freeze) the cropper.


### destroy()

Destroy the cropper and remove the instance from the image.


### move(offsetX[, offsetY])

- **offsetX**:
  - Type: `Number`
  - Moving size (px) in the horizontal direction.

- **offsetY** (optional):
  - Type: `Number`
  - Moving size (px) in the vertical direction.
  - If not present, its default value is `offsetX`.

Move the canvas (image wrapper) with relative offsets.

```js
$().cropper('move', 1);
$().cropper('move', 1, 0);
$().cropper('move', 0, -1);
```


### moveTo(x[, y])

- **x**:
  - Type: `Number`
  - The `left` value of the canvas

- **y** (optional):
  - Type: `Number`
  - The `top` value of the canvas
  - If not present, its default value is `x`.

Move the canvas (image wrapper) to an absolute point.


### zoom(ratio)

- **ratio**:
  - Type: `Number`
  - Zoom in: requires a positive number (ratio > 0)
  - Zoom out: requires a negative number (ratio < 0)

Zoom the canvas (image wrapper) with a relative ratio.

```js
$().cropper('zoom', 0.1);
$().cropper('zoom', -0.1);
```


### zoomTo(ratio)

- **ratio**:
  - Type: `Number`

Zoom the canvas (image wrapper) to an absolute ratio.

```js
$().cropper('zoom', 1); // 1:1 (canvasData.width === canvasData.naturalWidth)
```


### rotate(degree)

- **degree**:
  - Type: `Number`
  - Rotate right: requires a positive number (degree > 0)
  - Rotate left: requires a negative number (degree < 0)

Rotate the canvas (image wrapper) with a relative degree.

> Requires [CSS3 2D Transforms](http://caniuse.com/transforms2d) support (IE 9+).

```js
$().cropper('rotate', 90);
$().cropper('rotate', -90);
```


### rotateTo(degree)

- **degree**:
  - Type: `Number`

Rotate the canvas (image wrapper) to an absolute degree.


### scale(scaleX[, scaleY])

- **scaleX**:
  - Type: `Number`
  - Default: `1`
  - The scaling factor to apply on the abscissa of the image.
  - When equal to `1` it does nothing.

- **scaleY** (optional):
  - Type: `Number`
  - The scaling factor to apply on the ordinate of the image.
  - If not present, its default value is `scaleX`.

Scale the image.

> Requires [CSS3 2D Transforms](http://caniuse.com/transforms2d) support (IE 9+).

```js
$().cropper('scale', -1); // Flip both horizontal and vertical
$().cropper('scale', -1, 1); // Flip horizontal
$().cropper('scale', 1, -1); // Flip vertical
```


### scaleX(scaleX)

- **scaleX**:
  - Type: `Number`
  - Default: `1`
  - The scaling factor to apply on the abscissa of the image.
  - When equal to `1` it does nothing.

Scale the abscissa of the image.


### scaleY(scaleY)

- **scaleY**:
  - Type: `Number`
  - Default: `1`
  - The scaling factor to apply on the ordinate of the image.
  - When equal to `1` it does nothing.

Scale the ordinate of the image.


### getData([rounded])

- **rounded** (optional):
  - Type: `Boolean`
  - Default: `false`
  - Set `true` to get rounded values.

- (return value):
  - Type: `Object`
  - Properties:
    - `x`: the offset left of the cropped area
    - `y`: the offset top of the cropped area
    - `width`: the width of the cropped area
    - `height`: the height of the cropped area
    - `rotate`: the rotated degrees of the image
    - `scaleX`: the scaling factor to apply on the abscissa of the image
    - `scaleY`: the scaling factor to apply on the ordinate of the image

Output the cropped area position and size data (base on the original image).

![a schematic diagram of data's properties](assets/img/data.jpg)


### setData(data)

- **data**:
  - Type: `Object`
  - Properties: See the [`getData`](#getdatarounded) method.

Change the cropped area position and size with new data (base on the original image).

**Note:** Only available in strict mode.


### getContainerData()

- (return  value):
  - Type: `Object`
  - Properties:
    - `width`: the current width of the container
    - `height`: the current height of the container

Output the container size data.

![a schematic diagram of cropper's layers](assets/img/layers.jpg)


### getImageData()

- (return  value):
  - Type: `Object`
  - Properties:
    - `left`: the offset left of the image
    - `top`: the offset top of the image
    - `width`: the width of the image
    - `height`: the height of the image
    - `naturalWidth`: the natural width of the image
    - `naturalHeight`: the natural height of the image
    - `aspectRatio`: the aspect ratio of the image
    - `rotate`: the rotated degrees of the image if rotated
    - `scaleX`: the scaling factor to apply on the abscissa of the image if scaled
    - `scaleY`: the scaling factor to apply on the ordinate of the image if scaled

Output the image position, size and other related data.


### getCanvasData()

- (return  value):
  - Type: `Object`
  - Properties:
    - `left`: the offset left of the canvas
    - `top`: the offset top of the canvas
    - `width`: the width of the canvas
    - `height`: the height of the canvas
    - `naturalWidth`: the natural width of the canvas (read only)
    - `naturalHeight`: the natural height of the canvas (read only)

Output the canvas (image wrapper) position and size data.

```js
var imageData = $().cropper('getImageData');
var canvasData = $().cropper('getCanvasData');

if (imageData.rotate % 180 === 0) {
  console.log(canvasData.naturalWidth === imageData.naturalWidth); // true
}
```


### setCanvasData(data)

- **data**:
  - Type: `Object`
  - Properties:
    - `left`: the new offset left of the canvas
    - `top`: the new offset top of the canvas
    - `width`: the new width of the canvas
    - `height`: the new height of the canvas

Change the canvas (image wrapper) position and size with new data.


### getCropBoxData()

- (return  value):
  - Type: `Object`
  - Properties:
    - `left`: the offset left of the crop box
    - `top`: the offset top of the crop box
    - `width`: the width of the crop box
    - `height`: the height of the crop box

Output the crop box position and size data.


### setCropBoxData(data)

- **data**:
  - Type: `Object`
  - Properties:
    - `left`: the new offset left of the crop box
    - `top`: the new offset top of the crop box
    - `width`: the new width of the crop box
    - `height`: the new height of the crop box

Change the crop box position and size with new data.


### getCroppedCanvas([options])

- **options** (optional):
  - Type: `Object`
  - Properties:
    - `width`: the destination width of the output canvas
    - `height`: the destination height of the output canvas
    - `fillColor`: a color to fill any alpha values in the output canvas

- (return  value):
  - Type: `HTMLCanvasElement`
  - A canvas drawn the cropped image.

- Browser support:
  - Basic image: requires [Canvas](http://caniuse.com/canvas) support (IE 9+).
  - Rotated image: requires [CSS3 2D Transforms](http://caniuse.com/transforms2d) support (IE 9+).
  - Cross-origin image: requires HTML5 [CORS settings attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/CORS_settings_attributes) support (IE 11+).

Get a canvas drawn the cropped image.

> After then, you can display the canvas as an image directly, or use [canvas.toDataURL](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/toDataURL) to get a Data URL, or use [canvas.toBlob](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/toBlob) to get a blob and upload it to server with [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData) if the browser supports these APIs.

```js
$().cropper('getCroppedCanvas');

$().cropper('getCroppedCanvas', {
  width: 160,
  height: 90
});

// Upload cropped image to server
$().cropper('getCroppedCanvas').toBlob(function (blob) {
  var formData = new FormData();

  formData.append('croppedImage', blob);

  $.ajax('/path/to/upload', {
    method: "POST",
    data: formData,
    processData: false,
    contentType: false,
    success: function () {
      console.log('Upload success');
    },
    error: function () {
      console.log('Upload error');
    }
  });
});
```

### setAspectRatio(aspectRatio)

- **aspectRatio**:
  - Type: `Number`
  - Requires a positive number.

Change the aspect ratio of the crop box.


### setDragMode([mode])

- **mode** (optional):
  - Type: `String`
  - Default: `'none'`
  - Options: `'none'`, `'crop'`, `'move'`

Change the drag mode.

**Tips:** You can toggle the "crop" and "move" mode by double click on the cropper.



## Events

### build.cropper

This event fires when a cropper instance starts to load an image.


### built.cropper

This event fires when a cropper instance has built completely.


### cropstart.cropper

- **event.originalEvent**:
  - Type: `Event`
  - Options: `mousedown`, `touchstart` and `pointerdown`

- **event.action**:
  - Type: `String`
  - Options:
    - `'crop'`: create a new crop box
    - `'move'`: move the canvas (image wrapper)
    - `'zoom'`: zoom in / out the canvas (image wrapper) by touch.
    - `'e'`: resize the east side of the crop box
    - `'w'`: resize the west side of the crop box
    - `'s'`: resize the south side of the crop box
    - `'n'`: resize the north side of the crop box
    - `'se'`: resize the southeast side of the crop box
    - `'sw'`: resize the southwest side of the crop box
    - `'ne'`: resize the northeast side of the crop box
    - `'nw'`: resize the northwest side of the crop box
    - `'all'`: move the crop box (all directions)

This event fires when the canvas (image wrapper) or the crop box starts to change.

```js
$().on('cropstart.cropper', function (e) {
  console.log(e.type); // cropstart
  console.log(e.namespace); // cropper
  console.log(e.action); // ...
  console.log(e.originalEvent.pageX);

  // Prevent to start cropping, moving, etc if necessary
  if (e.action === 'crop') {
    e.preventDefault();
  }
});
```


### cropmove.cropper

- **event.originalEvent**:
  - Type: `Event`
  - Options: `mousemove`, `touchmove` and `pointermove`.

- **event.action**: the same as "cropstart.cropper".

This event fires when the canvas (image wrapper) or the crop box is changing.


### cropend.cropper

- **event.originalEvent**:
  - Type: `Event`
  - Options: `mouseup`, `touchend`, `touchcancel`, `pointerup` and `pointercancel`.

- **event.action**: the same as "cropstart.cropper".

This event fires when the canvas (image wrapper) or the crop box stops to change.


### crop.cropper

- **event.x**
- **event.y**
- **event.width**
- **event.height**
- **event.rotate**
- **event.scaleX**
- **event.scaleY**

> About these properties, see the [`getData`](#getdatarounded) method.

This event fires when the canvas (image wrapper) or the crop box changed.


### zoom.cropper

- **event.originalEvent**:
  - Type: `Event`
  - Options: `wheel`, `touchmove`.

- **event.oldRatio**:
  - Type: `Number`
  - The old ratio of the canvas

- **event.ratio**:
  - Type: `Number`
  - The new ratio of the canvas (`canvasData.width / canvasData.naturalWidth`)

This event fires when a cropper instance starts to zoom in or zoom out its canvas (image wrapper).

```js
$().on('zoom.cropper', function (e) {

  // Zoom in
  if (e.ratio > e.oldRatio) {

    // Prevent zoom in
    e.preventDefault();
  }

  // Zoom out
  // ...
});
```

## No conflict

If you have to use other plugin with the same namespace, just call the `$.fn.cropper.noConflict` method to revert to it.

```html
<script src="other-plugin.js"></script>
<script src="cropper.js"></script>
<script>
  $.fn.cropper.noConflict();
  // Code that uses other plugin's "$().cropper" can follow here.
</script>
```



## Browser support

- Chrome (latest 2)
- Firefox (latest 2)
- Internet Explorer 8+
- Opera (latest 2)
- Safari (latest 2)

As a jQuery plugin, you also need to see the [jQuery Browser Support](http://jquery.com/browser-support/).



## Contributing

Please read through our [contributing guidelines](CONTRIBUTING.md).



## Versioning

Maintained under the [Semantic Versioning guidelines](http://semver.org/).



## [License](LICENSE.md)

[MIT](http://opensource.org/licenses/MIT) © [Fengyuan Chen](http://github.com/fengyuanchen)



## Related projects

- [ngCropper](https://github.com/koorgoo/ngCropper) - AngularJS wrapper for Cropper.
- [react-cropper](https://github.com/roadmanfong/react-cropper) - Cropper as React components.
- [meteor-cropper](https://github.com/jonblum/meteor-cropper) - Cropper for Meteor.
- [ember-cli-cropper](https://github.com/anilmaurya/ember-cli-cropper) - Ember cli addon for Cropper.
- [ember-cli-image-cropper](https://github.com/mhretab/ember-cli-image-cropper) - Ember-cli addon for cropping/resizing images based on the jQuery Cropper plugin.
