# Swiper

[![Build Status](https://drone.io/github.com/marcojakob/dart-swiper/status.png)](https://drone.io/github.com/marcojakob/dart-swiper/latest)

A touch (and mouse) slider for swiping through images and HTML.


## Browser Support

Swiper supports all [browsers supported by Dart 1.6 and later]
(https://www.dartlang.org/support/faq.html#browsers-and-compiling-to-javascript):

* Internet Explorer, versions 10, and 11.
* Firefox, latest version.
* Chrome, latest version.
* Safari for desktop, version 6.
* Safari for mobile, version 6.


## Features

* **Touch and Mouse.** Slide either on a touch screen or with the mouse.
* **Smooth Transitions.** Swiper uses [Hardware-accelerated CSS3 transitions]
(http://blog.teamtreehouse.com/increase-your-sites-performance-with-hardware-accelerated-css) 
for smooth animations. 
* **Auto Resizing.** When the browser window is resized or a mobile device is 
rotated, the swiper and all its pages are resized automatically. 
* **Scroll Prevention.** Swiper detects if the user tries to slide or tries to 
scroll vertically.
* **Images or HTML.** Swiper supports any HTML content for swipe pages.


## Demos

*All Demos can be found in the `example` folder.*

* [Simple Example](http://marcojakob.github.io/dart-swiper/simple/)
* [Responsive Images Example](http://marcojakob.github.io/dart-swiper/responsive/)
* [Method and Events Example](http://marcojakob.github.io/dart-swiper/methods_events/)


## Usage

### 1. HTML

Swiper needs a simple HTML structure. Here is an example:

```HTML
<div class="swiper">
  <div class="page-container">
    <div></div>
    <div></div>
    <div></div>
  </div>
</div>
```

* The `swiper` is the main container. This will become the viewport.
* The `page-container` is the container that wraps all pages.
* The inner `div`s are the slide pages and can contain any HTML content.


### 2. Initialize the Swiper

In the Dart code you initialize the Swiper with a single line. The main 
container needs to be passed to the `Swiper` constructor.

```Dart
Swiper swiper = new Swiper(querySelector('.swiper'));
```


### 3. CSS

A few styles are needed:

```CSS
.swiper {
  overflow: hidden;
  position: relative;
  height: 333px; /* Declare the height of the swiper. */
  visibility: hidden; /* Hide until layout is ready. */
}

.page-container {
  position: relative;
  height: 100%;
}

.page-container > div {
  position: absolute;
  width: 100%;
}
```


## Constructor Options

* `startIndex`: the index position the Swiper should start at - *default: 0*
* `speed`: the speed of prev and next transitions in milliseconds - 
  *default: 300*
* `autoHeightRatio` defines if and how the Swiper should calculate the 
  height. If defined, the height is calculated from the swiper width with 
  `autoHeightRatio` and automatically applied when the browser is resized.
  This is useful, e.g. for responsive images - *default: null*
* `disableTouch`: defines if swiping with touch should be ignored. 
  *default: false*
* `disableMouse`: defines if swiping with mouse should be ignored. 
  *default: false*


#### Example

```Dart
Swiper swiper = new Swiper(querySelector('.swiper'), 
    startIndex: 2,
    speed: 600,
    autoHeightRatio: 0.66,
    disableTouch: false,
    disableMouse: false);
```


## Other Options

* `distanceThreshold`: If swipe distance is more than this threshold (in px), a 
  swipe is detected (regardless of swipe duration) - *default: 20*
* `durationThreshold`: If swipe duration is less than this threshold (in ms), a 
  swipe is detected (regardless of swipe distance) - *default: 250*
* `draggingClassSwiper`: CSS class set to the swiper element while a user is 
  dragging. If null, no css class is added - *default: swiper-dragging*
* `draggingClassBody`: CSS class set to the body tag while a user is 
  dragging. If null, no css class is added - *default: swiper-dragging*


#### Example

```Dart
Swiper swiper = new Swiper(querySelector('.swiper'));

swiper
    ..distanceThreshold = 40
    ..durationThreshold = 300
    ..draggingClassSwiper = 'my-dragging-class'
    ..draggingClassBody = null;
```


## Methods

* `currentIndex`: The current page index.
* `currentPage`: The HTML element of the current page.
* `moveToIndex(int index, {int speed, bool noEvents: false}`: Moves to the page 
  at the specified *index*. Optionally, the *speed* of the transition can be 
  specified. If no events (pageChange and pageTransitionEnd) should be fired, 
  the *noEvents* flag can be set to true.
* `next({int speed})`: Moves to the next page.
* `prev({int speed})`: Moves to the previous page.
* `hasNext()`: Returns true if there is a next page.
* `hasPrev()`: Returns true if there is a previous page.
* `resize()`: Updates the cached page width and the container sizes. The resize
  method is automatically called when the browser is resized. But if the Swiper
  is resized other than through browser resizing, the *resize* method must be 
  called manually.
* `destroy()`: Unistalls all listeners. This will return the swiper element 
  back to its pre-init state.


#### Example

```Dart
// Set up method calls for button clicks.
ButtonElement prevButton = querySelector('#previous-button')
    ..onClick.listen((_) => swiper.prev());
ButtonElement nextButton = querySelector('#next-button')
    ..onClick.listen((_) => swiper.next());
```

## Events

* `onPageChange`: Fired when the current page changed. The data of the event is 
  the page index.
* `onPageTransitionEnd`: Fired when the transition ends after a page change. 
  Note: when the user swipes again before the previous transition ended, this 
  event is only fired once, at the end of all page transitions. The data of the
  event is the page index.
* `onDragStart`: Fired when the user starts dragging.
* `onDrag`: Fired periodically throughout the drag operation.
* `onDragEnd`: Fired when the user ends the dragging.


#### Example

```Dart
swiper.onPageChange.listen((index) {
  print('PageChange Event: index=${index}');
});


## Attribution

Swiper is heavily inspiried by [flipsnap.js](https://github.com/pxgrid/js-flipsnap/), 
[swipe.js](https://github.com/bradbirdsall/Swipe), and
[SwipeView](https://github.com/cubiq/SwipeView).

Many thanks to the authors for those great JavaScript projects! 


## License
The MIT License (MIT)