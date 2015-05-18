#### Looking for help? Please post your questions to the [Slideshow Google Group](http://groups.google.com/group/mootools-slideshow)! ####



### How can I specify a directory for the thumbnail rather then appending a 't' to the image name? ###

_For example, the full-size image is "1.jpg" and the thumbnail "thumbs/1.jpg"._

You would need to modify the [replace](http://code.google.com/p/slideshow/wiki/Slideshow#Options:) option, something like:

```
'replace': [/^(.*)$/, 'thumbs/$1']
```

See [Regular Expressions](http://developer.mozilla.org/en/docs/Core_JavaScript_1.5_Reference:Global_Objects:RegExp) reference for more information.

### OK, but what if the images and thumbs are in two separate folders? ###

_For example, the full-size image is "slides/1.jpg" and the thumbnail "thumbs/1.jpg"._

You will have to use the parent folder "/" for [hu](http://code.google.com/p/slideshow/wiki/Slideshow#Options:), then prepend "slides/" to the image filenames:

```
data = [ 'slides/1.jpg', 'slides/2.jpg', ... ];
```

Then your replace would be something like:

```
replace = [/^slides(.*)$/, 'thumbs$1'];
```

### Is it possible to have multiple slideshows per page? ###

Sure. You will just need to give each wrapper element it's own ID, and initialize a new instance of the class for each one:

```
<div id="keylin" class="slideshow"><img src="keylin/1.jpg" alt="Keylin" /></div>
<div id="gustavo" class="slideshow"><img src="gustavo/1.jpg" alt="Gustavo" /></div>

<script type="text/javascript">
  window.addEvent('domready', function(){
    new Slideshow('keylin', ['1.jpg', '2.jpg', '3.jpg'], {height: 300, hu: 'keylin/', width: 400});
    new Slideshow('gustavo', ['1.jpg', '2.jpg', '3.jpg'], {height: 300, hu: 'gustavo/', width: 400});
  });
</script>
```

New! [See the example online](http://www.electricprism.com/aeron/slideshow/example6.html).

### Why does Slideshow disappear in Internet Explorer? ###

_While my slideshow works flawlessly in Safari and Firefox, both IE6 and IE7 do not display it properly. Instead, I merely see a brief "blip" of the default image, which then disappears, never to return._

The problem often is a trailing comma in the list of pictures, for example:

```
var data = {
  "img1.jpg":{caption:"Image 1"},
  "img2.jpg":{caption:"Image 2"},
};
```

In order to make it work in IE, just delete the last comma and write it like this:

```
var data = {
  "img1.jpg":{caption:"Image 1"},
  "img2.jpg":{caption:"Image 2"}
};
```

See the closing `}` after Image 2? No comma!

### Why is Slideshow so slow to load in Internet Explorer 6? ###

_My implementation of Slideshow takes about 30 seconds to load in IE6, while in every other browser (IE7, FF, Safari, etc) it loads very fast._

The problem is if you are using the optional [loader](http://code.google.com/p/slideshow/wiki/Slideshow#Options:) but the path to the loading image(s) is incorrect. In this case simply set `loader: false`.

### How can I resize the Slideshow? ###

_I am having trouble resizing the div - I don't see it anywhere in the Slideshow CSS._

Since height and width are attributes of the presentation, it is best to change these values in the stylesheet:

```
.slideshow-images {
  height: 300px;
  width: 400px;
}
```

Slideshow will parse in these values on initialization and adjust the dimensions of the show accordingly. You can also do the same thing in reverse by setting the options in the Slideshow class:

```
new Slideshow('show', data, { height: 300, hu: 'images/', width: 400 });
```

The only difference is the show will only take those dimensions if Javascript is enabled. Note: these attributes only affect the size of the "slides" or Slideshow images (more information [in the Wiki](http://code.google.com/p/slideshow/wiki/HTML)):

```
<div class="slideshow">
  <div class="slideshow-images">
    <a><img /></a>
  </div>
 ...
</div>
```

In order to affect the dimensions of the Slideshow wrapper (that contains the controller, captions, thumbnails, etc) you will need to set the following class in the stylesheet:

```
.slideshow {
  height: 300px;
  width: 400px;
}
```

Accordingly, the size of the Slideshow images will not be affected.

### Why won't Slideshow work with Google Maps? ###

_I load a page with Google Maps, Mootools 1.2 and Slideshow and initiate a Slideshow and a Map on their own DIVs and Firebug reports:_

```
"A parameter or an operation is not supported by the underlying object" code: 15 /scripts/mootools_core.js Line 3162
```

This is a Google Maps issue. Simply loading the Maps CSS after the Javascript gives this error. Placing the CSS file before the Javascript was included fixed it.

### When I use PNG images with an alpha channel the previous image can be seen behind the current one? ###

_I only want to see the current image - the previous image should be gone._

Initialize Slideshow with the [overlap: false](http://code.google.com/p/slideshow/wiki/Slideshow#Options:) option.

### Why aren't the Slideshow animations working correctly? ###

_Either the main image isn't appearing or the captions (loader, controller, etc) are not animating as I have specified in the `slideshow.css`._

In this case there may be a problem that Mootools is unable to access the Slideshow stylesheet. This can happen for either of two reasons:

  * You are using **the `@import` method** to import the Slideshow CSS. Unfortunately this method will not allow Mootools access to the stylesheet. In this case switch to using the traditional [link tag](http://www.w3.org/TR/REC-html40/present/styles.html#h-14.1) from within the head of the HTML document that contains the Slideshow instance.
  * Your stylesheet is **on a different domain (or subdomain)** than the page which contains the Slideshow instance. Unfortunately security restrictions in Javascript will prevent Mootools from accessing the styleheet. You will need to move the slideshow.css to the same domain as the HTML document which contains the Slideshow instance or use a relative path (sorta the same thing).

### Why does the Ken Burns Slideshow look so bad on IE / PC? ###

_[Great tool but IE performance suffers a little too much for me to use it for professional work](http://forum.mootools.net/viewtopic.php?id=1673&p=3#post-17571)._

This has been fixed for IE7 since rev 131 - get the [latest version here](http://code.google.com/p/slideshow/downloads/list). Unfortunately there doesn't appear to be any fix for IE6. However at the moment the Slideshow should look awesome on IE7/8, Firefox 3+, Chrome/Safari and any Mac browser!

### Why can I not see anything? ###

_I get the error: Asset is not defined_

If you are using Slideshow with a different version of Mootools than the one included with the class, be sure to also add the [Assets utility](http://www.mootools.net/more#Assets). Slideshow requires the Assets utility to stream in images and will not work without it.

### How can I have the image links open in a new window? ###

_Is there a way to set the `target` attribute?_

Slideshow will inherit any properties already existing in the html. So if your html looks like this:
```
<div class="slideshow"> 
  <a href="http://www.somewhere.com" target="_blank"> 
    <img src="1.jpg"> 
  </a> 
</div> 
```
Then all the links in your slideshow will inherit the target attribute.