#### Looking for help? Please post your questions to the [Slideshow Google Group](http://groups.google.com/group/mootools-slideshow)! ####



The following represents the structure of the HTML Slideshow constructs upon initialization:

```
<div class="slideshow">
  <div class="slideshow-images">
    <a><img /></a>
    <div class="slideshow-loader"></div>
  </div>

  <div class="slideshow-captions"></div>

  <div class="slideshow-controller">
    <ul>
      <li class="first"><a></a></li>
      <li class="prev"><a></a></li>
      <li class="pause play"><a></a></li>
      <li class="next"><a></a></li>
      <li class="last"><a></a></li>
    </ul>
  </div>

  <div class="slideshow-thumbnails">
    <ul>
      <li><a class="slideshow-thumbnails-active"><img /></a></li>
      <li><a class="slideshow-thumbnails-inactive"><img /></a></li>
      <li><a class="slideshow-thumbnails-inactive"><img /></a></li>
      ...
    </ul>
  </div>
</div>
```

#### Notes: ####

  * If the above structure exists in your HTML document prior to Slideshow initialization, the class will merely parse in the pre-existing code, preserving values with the following behavior:
    * Attributes of the anchor inside `<div class="slideshow-images">` will be preserved. The `href` (if existing) will become the default hyperlink for the show. Apply a `rel` attribute to use the Slideshow with Lightbox, Slimbox, etc.
    * If a `null` data array is passed to Slideshow on initialization it will attempt to parse images from within `<div class="slideshow-images">` (if existing). In such case, the image `alt` attributes will become the captions for the show. In addition it will attempt to parse thumbnails from within `<div class="slideshow-thumbnails">` associating each thumbnail with the corresponding full-size image.
  * In the Slideshow controller, the `pause` class corresponds to the pause icon. When a show is playing the pause icon is shown to indicate clicking will pause the presentation. The `play` class - corresponding to the play icon - is appended to the pause element when a show has been stopped (as in the above example) an indication that clicking will resume the presentation.
  * All CSS classes are generated from the values in the classes array of the Slideshow options object (see [Notes](http://code.google.com/p/slideshow/wiki/Slideshow#Notes:)). Merely changing the first class of the array will affect all classes generated: `classes: ['gallery']` will result in HTML such as `<div class="gallery-images">` etc.