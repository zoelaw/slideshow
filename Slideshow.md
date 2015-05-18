#### Looking for help? Please post your questions to the [Slideshow Google Group](http://groups.google.com/group/mootools-slideshow)! ####



### Method: constructor ###

Creates an instance of the Slideshow class. Applied to an existing element(s) in the HTML. Can parse in existing images, alt attributes, thumbnails, etc. or create as necessary.

#### Syntax: ####

```
var myShow = new Slideshow(element, data, options);
```

#### Arguments: ####

  1. element - (element) The wrapper element.
  1. data - (array or object) The images and optional thumbnails, captions and links for the show.
  1. options - (object) The options below.

#### Options: ####

  * accesskeys - (object) Object of custom key/label combinations for accessibility accesskeys. The "key" can be any combination of alphanumeric keys and/or modifiers (one of shift, control or alt) separated by commas. The "label" can be any localized text that will appear as a tooltip.
  * captions<sup>1</sup> - (boolean or Fx options object: default false) Whether to show captions.
  * center<sup>2</sup> - (boolean: default true) Whether the show should attempt to center images.
  * classes<sup>3</sup>  - (array) An array of CSS class names to use with styling the show.
  * controller<sup>1</sup> - (boolean or Fx options object: default false) Whether to show controller.
  * delay - (integer: default 2000) The delay between slide changes in milliseconds (1000 = 1 second).
  * duration - (integer: default 750) The duration of the effect in milliseconds (1000 = 1 second).
  * fast - (boolean, integer or one of the named constants) Originally related to "fast mode" a slideshow mode where transitions were skipped. The named constants are WhenPaused, WhenPlaying and OnStart and can be combined using the bitwise OR operator | (a single bar). For example, fast = WhenPaused tells Slideshow to skip transitions when the user navigates a paused show. Or, fast = WhenPaused | WhenPlaying tells slideshow to always skip transitions when the user navigates the show.
  * height - (boolean or integer: default false) Optional height value for the show as a whole integer, if a height value is not given the height of the default image will be used.
  * href - (string: default empty) A single link for the show, inherited from the HTML href of the default image.
  * hu - (string) Path to the image directory, relative or absolute, default is the root directory of the website, use an empty string for the same directory as the webpage.
  * linked - (boolean: default false) Whether the class should automatically link each slide to the fullsize image, useful when mashing Slideshow with Slimbox, Lightbox, etc.
  * loader<sup>1</sup> - (boolean or Fx options object: default object) Show the loader graphic for images being loaded.
  * loop - (boolean: default true) Should the show loop.
  * match - (regexp) A regular expression the class uses to parse the URL, will overwrite "slide" below, default looks for `?slide=n` where "n" would be the slide to start from.
  * onStart, onComplete, onEnd - (function) Events that are fired on the start or completion of a slide change and at the end of a non-looping show.
  * overlap - (boolean: default true) Whether images overlap in the basic show, or if the first image transitions out before the second transitions in.
  * paused - (boolean: default false) Whether the show should start paused.
  * random - (boolean: default false) Random show, combined with thumbnails equals very cool!
  * replace - (array) An array, consisting of a regular expression pattern and a string replacement, for building thumbnail filenames based on the name of the original image, default appends a "t" to the image filename before the extension.
  * resize - (boolean or string: default "fill") Whether the show should attempt to resize images, based on the shortest side (default) or longest side ("fit") or resize without preserving proportions ("stretch"). Set to false to disable image resizing.
  * slide - (integer: default 0) Slide from which to start the show.
  * thumbnails<sup>1</sup> - (boolean or Fx options object: default false) Whether to show thumbnails.
  * titles - (boolean) Whether to use captions for image and thumbnail title attributes.
  * transition - (function: default Sine) Transition to use with base and push type shows (requires Mootools with Fx.Transitions).
  * width - (boolean or integer: default false) Optional width value for the show as a whole integer, if a width value is not given the width of the default image will be used.

#### Returns: ####

  * (object) A new Slideshow instance.

#### Examples: ####

  * Example A: example data object with all available parameters.

```
var data = {
  // In this case no thumbnail has been specified so Slideshow will generate the thumbnail filename from the image using the RegExp defined in the replace option
  '1.jpg': {
    caption: 'Keylin', 
    href: 'keylin.html'
  },
  // Here the image and thumbnail use the same filename but different directories and an example of captions with HTML
  'images/2.jpg': {
    caption: '<em>Gustavo</em>', 
    href: 'gustavo.html',
    thumbnail: 'thumbs/2.jpg'
  },
  // In this example the image and thumbnail use absolute filenames
  'http://images.mysite.com/images/3.jpg': {
    caption: 'Amalia',
    thumbnail: 'http://images.mysite.com/thumbs/2.jpg'
  }
};
```

  * Example 1: data passed in as an array; show is linked to a static url (href: 'portfolio.html').

```
<div id="my_show" class="slideshow">
  <img src="1.jpg" alt="Keylin" />
</div>

<script type="text/javascript">
  var data = ['1.jpg', '2.jpg', '3.jpg'];

  var myShow = new Slideshow('my_show', data, {href: 'portfolio.html', hu: 'images/'});
</script>
```

  * Example 2: data passed in as an object with captions and links for each image; controller customized with an Fx options object.

```
<div id="my_show" class="slideshow">
  <img src="1.jpg" alt="Keylin" />
</div>

<script type="text/javascript">
  var data = {'1.jpg': {caption: 'Keylin', href: 'keylin.html'}, '2.jpg': {caption: 'Gustavo', href: 'gustavo.html'}, '3.jpg': {caption: 'Amalia', href: 'amalia.html'}};

  var myShow = new Slideshow('my_show', data, {captions: true, controller: {duration: 1000, transition: 'elastic:in:out'}, hu: 'images/'});
</script>
```

  * Example 3: data passed in as an array; slides are auto-linked to the full-size image (linked: true); there is a default anchor in the HTML with a REL attribute (rel="lightbox"), this attribute will be duplicated for all auto-generated links allowing for easy pairing with a 3rd-party Lightbox script.

```
<div id="my_show" class="slideshow">
  <a rel="lightbox" href="1.jpg"><img src="1.jpg" alt="Keylin" /></a>
</div>

<script type="text/javascript">
  var data = ['1.jpg', '2.jpg', '3.jpg'];

  var myShow = new Slideshow('my_show', data, {controller: true, hu: 'images/', linked: true});
</script>
```


#### Notes: ####

  * <sup>1</sup> Captions, controller, loader and thumbnails all accept either a boolean (true / false) or [options object](http://mootools.net/docs/core/Fx/Fx) to customize element effect.
  * <sup>2</sup> Centering will not work as anticipated if the CSS classes used to define the effects of the show include absolute positioning. For this reason, it is recommended to use image margins to animate slide changes. For a demonstration, please consult the [example](http://www.electricprism.com/aeron/slideshow/example3.html).
  * <sup>3</sup> Internally the classes are in the following order: `['slideshow', 'first', 'prev', 'play', 'pause', 'next', 'last', 'images', 'captions', 'controller', 'thumbnails', 'hidden', 'visible', 'inactive', 'active', 'loader']`. Therefore if you wanted to change the name of the classes used for the controller (which also affects the HTML titles used for the controls themselves) you would set: `classes: ['',  'primero', 'anterior', 'comenza', 'pausa', 'proximo', 'ultimo']`. Class names left empty or not specified will use the Slideshow defaults.


### Method: load ###

Loads a new data set into the show: will stop the current show, rewind and rebuild thumbnails if applicable.

#### Syntax: ####

```
myShow.load(data);
```

#### Arguments: ####

  1. data - (array or object) The images and optional thumbnails, captions and links for the show.

#### Returns: ####

  * (integer) Number of images loaded.


### Method: destroy ###

Destroys the current slideshow instance: removes global events, clears callbacks, frees memory.

#### Syntax: ####

```
myShow.destroy(p);
```

#### Arguments: ####

  1. p - (string) Optional parameter indicating desired action for existing show HTML. Upon destruction the dynamic HTML of a show becomes static, non-interactive. Call destroy with the parameter `empty` to remove all existing HTML _inside_ of the show - useful to then apply a new Slideshow instance to the same wrapper element. Call destroy with the parameter `dispose` to remove all existing HTML _and_ the wrapper element - useful to completely remove a Slideshow instance from the page.


### Method: first ###

Goes to the first image in the show.

#### Syntax: ####

```
myShow.first();
```


### Method: prev ###

Goes to the previous image in the show.

#### Syntax: ####

```
myShow.prev();
```


### Method: pause ###

Toggles play / pause state of the show.

#### Syntax: ####

```
myShow.pause(p);
```

#### Arguments: ####

  1. p - (undefined, 1 or 0) Call pause with no arguments to toggle the pause state. Call pause(1) to force pause, or pause(0) to force play.


### Method: next ###

Goes to the next image in the show.

#### Syntax: ####

```
myShow.next();
```


### Method: last ###

Goes to the last image in the show.

#### Syntax: ####

```
myShow.last();
```


### Method: go ###

Jump directly to a slide in the show.

#### Syntax: ####

```
myShow.go(n);
```

#### Arguments: ####

  1. n - (integer) The index number of the image to jump to, 0 being the first image in the show.


### Property: slide ###

Number of current slide.


#### Syntax: ####

```
myShow.slide;
```