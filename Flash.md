#### Looking for help? Please post your questions to the [Slideshow Google Group](http://groups.google.com/group/mootools-slideshow)! ####



#### Extends: ####

[Slideshow](http://code.google.com/p/slideshow/wiki/Slideshow)

### Method: constructor ###

Creates a flashing slideshow: each transition begins with a flat color that fades into the image.

#### Syntax: ####

```
var myShow = new Slideshow.Flash(element, data, options);
```

#### Arguments: ####

  1. element - (element) The slideshow wrapper element.
  1. data - (array or object) The images, thumbnails, captions and links for the slideshow.
  1. options - (object) All of the [Slideshow](http://code.google.com/p/slideshow/wiki/Slideshow) options in addition to the options below.

#### Options: ####

  * color - (string or array: default #FFF) A single color: "#FFF", or an array of colors: ["#FFF", "#000"], which are applied incrementally to the slides in the show.