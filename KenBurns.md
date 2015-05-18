#### Looking for help? Please post your questions to the [Slideshow Google Group](http://groups.google.com/group/mootools-slideshow)! ####



#### Extends: ####

[Slideshow](http://code.google.com/p/slideshow/wiki/Slideshow)

### Method: constructor ###

Creates a Ken Burns slideshow with zooming and panning effects.

#### Syntax: ####

```
var myShow = new Slideshow.KenBurns(element, data, options);
```

#### Arguments: ####

  1. element - (element) The slideshow wrapper element.
  1. data - (array or object) The images, thumbnails, captions and links for the slideshow.
  1. options - (object) All of the [Slideshow](http://code.google.com/p/slideshow/wiki/Slideshow) options in addition to the options below.

#### Options: ####

  * pan<sup>1</sup> - (integer or array: default 100) An integer, or range of integers as an array, from 0 to 100 that pans the slide 0% to 100% of it's overflow.
  * zoom<sup>2</sup> - (integer or array: default 50) An integer, or range of integers as an array, from 0 to 100 that zooms the slide 1× to 2× of the size of the slideshow.

#### Examples: ####

```
<div id="my_show" class="slideshow">
  <img src="1.jpg" alt="Keylin" />
</div>

<script type="text/javascript">
  var myShow = new Slideshow.KenBurns('my_show', ['1.jpg', '2.jpg', '3.jpg'], {pan: 100, zoom: [25, 75]});
</script>
```

#### Notes: ####

  * <sup>1</sup> There is no [sub-pixel](http://ejohn.org/blog/sub-pixel-problems-in-css/) positioning in any browser, so the quality of the panning is determined by how much the image will pan: an image that pans a lot (ie. a rectangular image in a square slideshow) will animate smoother.
  * <sup>2</sup> The zooming effect is very dependent on the operating system (ie. Windows, Mac, Linux, etc) since the OS is what determines the resampling algorithm used by the browser. In general, any browser on Mac will scale much better. See [this FAQ](http://code.google.com/p/slideshow/wiki/FAQ#Why_does_the_Ken_Burns_Slideshow_look_so_bad_on_IE_/_PC?) for more information.