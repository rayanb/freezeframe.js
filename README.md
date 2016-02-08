## freezeframe.js

freezeframe.js is a script that pauses animated .gifs and enables them to 
animate automatically on mouse hover / mouse click / touch event, or manually 
with trigger / release functions. It supports responsive images and works as a 
jQuery plugin.

1. [Examples](#examples)
2. [Files & Dependencies](#files_dependencies)
3. [Basic Usage: jQuery Plugin](#basic_usage_jquery_plugin)
4. [Basic Usage: Vanilla JS](#basic_usage_vanilla_js)
5. [Advanced Usage](#advanced_usage)
6. [Options Reference](#options_reference)
7. [Function Reference](#function_reference)

<a name="examples"></a>
## Examples
[http://ctrl-freaks.github.io/freezeframe.js/](http://ctrl-freaks.github.io/freezeframe.js/)

<a name="files_dependencies"></a>
## Files & Dependencies

1. Include the js and css from **/build/**  

    ```
  <link rel="stylesheet" href="freezeframe_styles.min.css">
  <script src="freezeframe.min.js"></script>
    ```
2. If you do not use a **packaged version** the following dependencies are required. These files can be found in **/src/js/vendor/**:
  * imagesLoaded Packaged v4.0.0 ( [https://github.com/desandro/imagesloaded](https://github.com/desandro/imagesloaded) )
  * jQuery

<a name="basic_usage_jquery_plugin"></a>
## Basic Usage: jQuery Plugin

1. Capture the image you want by selector and run the **freezeframe()** function.  

    ```javascript
  $('.my_class').freezeframe();
    ```

<a name="basic_usage_vanilla_js"></a>
## Basic Usage: Vanilla JS

1. Add **freezeframe** as a class name on the .gifs you want processed.
    ```
  <img class="freezeframe" src="image.gif" /> 
    ```
  Add **freezeframe-responsive** as an additional class name to make the .gif responsive.
    ```
  <img class="freezeframe freezeframe-responsive" src="image.gif" /> 
    ```

2. ✨ Freeze those frames ✨

    ```javascript
  $(function() {
    ff = new freezeframe().freeze();
  })
    ```

<a name="advanced_usage"></a>
## Advanced Usage

freezeframe.js exposes public methods to allow for more custom integration. You 
have the option of manually controlling when freezeframe captures images, adds 
support elements, and attaches event handlers. You can also manually trigger 
and release animation on one image or a group of images. These methods are 
described in detail in the [Function Reference](#function_reference).

Capture .gifs and manually trigger / release animation:
```javascript
logo = new freezeframe('#logo'); // setup freezeframe instance with custom selector

logo.capture(); // capture images by selector
logo.setup();   // setup support elements
logo.trigger(); // trigger animation
logo.release(); // release animation
```

<a name="options_reference"></a>
## Options Reference

Options can be passed to a freezeframe instance on creation in the form of an 
**object** or a **string**. Strings will be interpreted as the **selector** option.  

```javascript
// Options passed to jQuery plugin
$('.my_class').freezeframe({'animation_play_duration': 2500})

// String as selector option
var ff = new freezeframe('.my_class');

// Object as options
var ff = new freezeframe({
  'selector': '.my_class',
  'animation_play_duration': 3000,
  'non_touch_device_trigger_event': 'hover'
})
```

* **selector** *string*  
    Default: ```".freezeframe"```  
    The selector freezeframe will use to search for .gifs when the capture() 
    function is run (if no custom selector is passed to the capture() function).

* **animation_play_duration** *integer*  
    Default: ```5000```  
    The number of milliseconds a .gif will animate for when triggered by click / touch event.

* **non_touch_device_trigger_event** *string*  
    Default: ```"hover"``` Options: ```"hover", "click"```  
    The trigger event to start animation for non-touch devices.

<a name="function_reference"></a>
## Function Reference

* **freezeframe(** options **)**  
    Creates a new freezeframe object instance. Can be passed options.
     ```javascript
  // Default options
  var ff = new freezeframe();

  // String as selector option
  var ff = new freezeframe('.my_class');

  // Object as options
  var ff = new freezeframe({
    'selector': '.my_class',
    'animation_play_duration': 3000,
    'non_touch_device_trigger_event': 'hover'
  })
    ```

* **capture(** selector **)**  
    Captures images to be paused by freezeframe. If run without selector 
    argument, selector in freezeframe options will be used. Can be run multiple 
    times with different selector to group many images, unrelated by selector, 
    in one freezeframe instance.
    ```javascript
  ff.capture();               // use selector in freezeframe options
  ff.trigger('.my_class');    // use custom selector
    ```

* **setup()**   
    Creates and inserts support elements. Can be filtered by selector.  
    ```javascript
  ff.setup();                 // all images in freezeframe instance
  ff.setup('.my_class');      // filter images by selector
    ```
    HTML image before:

     ```
  <img class="freezeframe" src="my_image.gif" />
     ```  

     ...and after:
     ```
  <div class="ff-container">
    <canvas class="ff-canvas ff-canvas-ready" width="400" height="250"></canvas>
    <img class="freezeframe ff-setup ff-image ff-image-ready" src="my_image.gif">
  </div>
     ```

* **attach(** selector **)**  
    Attaches hover / click / touch events based on freezeframe options.
    ```javascript
  ff.attach();                // all images in freezeframe instance
  ff.attach('.my_class');     // filter images by selector
    ```

* **trigger(** selector **)**  
    Triggers (starts) animation. Can be filtered by selector.
    ```javascript
  ff.trigger();               // all images in freezeframe instance
  ff.trigger('.my_class');    // filter images by selector
    ```

* **release(** selector **)**  
    Releases (stops) animation.
    ```javascript
  ff.release()                // all images in freezeframe instance
  ff.release('.my_class');    // filter images by selector
    ```