# reveal.js ![tests](https://github.com/hakimel/reveal.js/workflows/tests/badge.svg) <a href="https://slides.com?ref=github"><img src="https://s3.amazonaws.com/static.slid.es/images/slides-github-banner-320x40.png?1" alt="Slides" width="160" height="20"></a>

A framework for easily creating beautiful presentations using HTML. [Check out the live demo](https://revealjs.com/).

reveal.js comes with a broad range of features including [nested slides](https://github.com/hakimel/reveal.js#markup), [Markdown support](https://github.com/hakimel/reveal.js#markdown), [PDF export](https://github.com/hakimel/reveal.js#pdf-export), [speaker notes](https://github.com/hakimel/reveal.js#speaker-notes) and a [JavaScript API](https://github.com/hakimel/reveal.js#api). There's also a fully featured visual editor and platform for sharing reveal.js presentations at [slides.com](https://slides.com?ref=github).

### Supporting reveal.js
This project was started and is maintained by [@hakimel](https://github.com/hakimel/) with the help of many [contributions from the community](https://github.com/hakimel/reveal.js/graphs/contributors). The best way to support the project is to [become a paying member of Slides.com](https://slides.com/pricing)—the reveal.js presentation platform that Hakim is building.


## Table of contents

- [Online Editor](#online-editor)
- [Installation](#installation)
  - [Basic setup](#basic-setup)
  - [Full setup](#full-setup)
- [Markup](#markup)
- [Initialization](#initialization)
- [Configuration](#configuration)
- [Presentation Size](#presentation-size)
- [Ready Event](#ready-event)
- [Auto-Slide](#auto-slide)
- [Auto-Animate](#auto-animate)
- [Keyboard Bindings](#keyboard-bindings)
- [Vertical Slide Navigation](#vertical-slide-navigation)
- [Touch Navigation](#touch-navigation)
- [Lazy Loading](#lazy-loading)
- [Plugins](#plugins)
- [Dependencies](#dependencies)
- [API](#api)
  - [Custom Key Bindings](#custom-key-bindings)
  - [Slide Change Events](#slide-change-events)
  - [Presentation State](#presentation-state)
  - [Slide States](#slide-states)
  - [Slide Backgrounds](#slide-backgrounds)
  - [Parallax Background](#parallax-background)
  - [Slide Transitions](#slide-transitions)
  - [Internal links](#internal-links)
  - [Fragments](#fragments)
  - [Fragment events](#fragment-events)
  - [Code syntax highlighting](#code-syntax-highlighting)
  - [Slide number](#slide-number)
  - [Overview mode](#overview-mode)
  - [Fullscreen mode](#fullscreen-mode)
  - [Embedded media](#embedded-media)
  - [Stretching elements](#stretching-elements)
  - [Resize Event](#resize-event)
  - [postMessage API](#postmessage-api)
- [Markdown](#markdown)
  - [External Markdown](#external-markdown)
  - [Element Attributes](#element-attributes)
  - [Slide Attributes](#slide-attributes)
- [PDF Export](#pdf-export)
- [Theming](#theming)
- [Speaker Notes](#speaker-notes)
  - [Share and Print Speaker Notes](#share-and-print-speaker-notes)
  - [Server Side Speaker Notes](#server-side-speaker-notes)
- [Multiplexing](#multiplexing)
- [MathJax](#mathjax)
- [License](#license)

#### More reading

- [Changelog](https://github.com/hakimel/reveal.js/releases): Up-to-date version history.
- [Examples](https://github.com/hakimel/reveal.js/wiki/Example-Presentations): Presentations created with reveal.js, add your own!
- [Browser Support](https://github.com/hakimel/reveal.js/wiki/Browser-Support): Explanation of browser support and fallbacks.
- [Plugins](https://github.com/hakimel/reveal.js/wiki/Plugins,-Tools-and-Hardware): A list of plugins that can be used to extend reveal.js.


## Online Editor

Presentations are written using HTML or Markdown but there's also an online editor for those of you who prefer a graphical interface. Give it a try at [https://slides.com](https://slides.com?ref=github).



### Initialization

If you only have a single presentation on the page we recommend initializing reveal.js using the singleton API.
```html
<script src="dist/reveal.es5.js"></script>
<script>
  Reveal.initialize({ keyboard: true });
</script>
```

The `initialize` method returns a promise which will resolve as soon as the presentation is ready and can be interacted with via the API.
```js
Reveal.initialize.then( () => {
  // reveal.js is ready
} )
```

If you want to run multiple presentations side-by-side on the same page you can create instances of the Reveal class. Note that you will also need to set the `embedded` config option to true.
```html
<div class="reveal deck-1">...</div>
<div class="reveal deck-2">...</div>
<script src="dist/reveal.es5.js"></script>
<script>
  let deck1 = new Reveal( document.querySelector( 'deck-1' ), { embedded: true } );
  let deck2 = new Reveal( document.querySelector( 'deck-2' ), { embedded: true } );

  deck1.initialize();
  deck2.initialize();
</script>
```

### ES Module

We provide two JavaScript bundles; `/dist/reveal.es5.js` with support for legacy browers and `/dist/reveal.js` which targets modern browsers with ES6 support.

Here's how to import and initialize the ES module version of reveal.js, including the Markdown plugin:

```html
<script type="module">
  import Reveal from '/dist/reveal.js';
  import Markdown from '/plugin/markdown/markdown.js';
  Reveal.initialize({
    plugins: [ Markdown ]
  });
</script>
```

### Configuration

At the end of your page you need to initialize reveal by running the following code. Note that all configuration values are optional and will default to the values specified below.

```javascript
Reveal.initialize({

  // Display presentation control arrows
  controls: true,

  // Help the user learn the controls by providing hints, for example by
  // bouncing the down arrow when they first encounter a vertical slide
  controlsTutorial: true,

  // Determines where controls appear, "edges" or "bottom-right"
  controlsLayout: 'bottom-right',

  // Visibility rule for backwards navigation arrows; "faded", "hidden"
  // or "visible"
  controlsBackArrows: 'faded',

  // Display a presentation progress bar
  progress: true,

  // Display the page number of the current slide
  slideNumber: false,

  // Add the current slide number to the URL hash so that reloading the
  // page/copying the URL will return you to the same slide
  hash: false,

  // Push each slide change to the browser history. Implies `hash: true`
  history: false,

  // Enable keyboard shortcuts for navigation
  keyboard: true,

  // Enable the slide overview mode
  overview: true,

  // Vertical centering of slides
  center: true,

  // Enables touch navigation on devices with touch input
  touch: true,

  // Loop the presentation
  loop: false,

  // Change the presentation direction to be RTL
  rtl: false,

  // See https://github.com/hakimel/reveal.js/#navigation-mode
  navigationMode: 'default',

  // Randomizes the order of slides each time the presentation loads
  shuffle: false,

  // Turns fragments on and off globally
  fragments: true,

  // Flags whether to include the current fragment in the URL,
  // so that reloading brings you to the same fragment position
  fragmentInURL: true,

  // Flags if the presentation is running in an embedded mode,
  // i.e. contained within a limited portion of the screen
  embedded: false,

  // Flags if we should show a help overlay when the questionmark
  // key is pressed
  help: true,

  // Flags if speaker notes should be visible to all viewers
  showNotes: false,

  // Global override for autoplaying embedded media (video/audio/iframe)
  // - null: Media will only autoplay if data-autoplay is present
  // - true: All media will autoplay, regardless of individual setting
  // - false: No media will autoplay, regardless of individual setting
  autoPlayMedia: null,

  // Global override for preloading lazy-loaded iframes
  // - null: Iframes with data-src AND data-preload will be loaded when within
  //   the viewDistance, iframes with only data-src will be loaded when visible
  // - true: All iframes with data-src will be loaded when within the viewDistance
  // - false: All iframes with data-src will be loaded only when visible
  preloadIframes: null,

  // Can be used to globally disable auto-animation
  autoAnimate: true,

  // Optionally provide a custom element matcher that will be
  // used to dictate which elements we can animate between.
  autoAnimateMatcher: null,

  // Default settings for our auto-animate transitions, can be
  // overridden per-slide or per-element via data arguments
  autoAnimateEasing: 'ease',
  autoAnimateDuration: 1.0,
  autoAnimateUnmatched: true,

  // CSS properties that can be auto-animated. Position & scale
  // is matched separately so there's no need to include styles
  // like top/right/bottom/left, width/height or margin.
  autoAnimateStyles: [
    'opacity',
    'color',
    'background-color',
    'padding',
    'font-size',
    'line-height',
    'letter-spacing',
    'border-width',
    'border-color',
    'border-radius',
    'outline',
    'outline-offset'
  ],

  // Number of milliseconds between automatically proceeding to the
  // next slide, disabled when set to 0, this value can be overwritten
  // by using a data-autoslide attribute on your slides
  autoSlide: 0,

  // Stop auto-sliding after user input
  autoSlideStoppable: true,

  // Use this method for navigation when auto-sliding
  autoSlideMethod: Reveal.next,

  // Specify the average time in seconds that you think you will spend
  // presenting each slide. This is used to show a pacing timer in the
  // speaker view
  defaultTiming: 120,

  // Specify the total time in seconds that is available to
  // present.  If this is set to a nonzero value, the pacing
  // timer will work out the time available for each slide,
  // instead of using the defaultTiming value
  totalTime: 0,

  // Specify the minimum amount of time you want to allot to
  // each slide, if using the totalTime calculation method.  If
  // the automated time allocation causes slide pacing to fall
  // below this threshold, then you will see an alert in the
  // speaker notes window
  minimumTimePerSlide: 0,

  // Enable slide navigation via mouse wheel
  mouseWheel: false,

  // Hide cursor if inactive
  hideInactiveCursor: true,

  // Time before the cursor is hidden (in ms)
  hideCursorTime: 5000,

  // Opens links in an iframe preview overlay
  // Add `data-preview-link` and `data-preview-link="false"` to customise each link
  // individually
  previewLinks: false,

  // Transition style
  transition: 'slide', // none/fade/slide/convex/concave/zoom

  // Transition speed
  transitionSpeed: 'default', // default/fast/slow

  // Transition style for full page slide backgrounds
  backgroundTransition: 'fade', // none/fade/slide/convex/concave/zoom

  // Number of slides away from the current that are visible
  viewDistance: 3,

  // Number of slides away from the current that are visible on mobile
  // devices. It is advisable to set this to a lower number than
  // viewDistance in order to save resources.
  mobileViewDistance: 2,

  // Parallax background image
  parallaxBackgroundImage: '', // e.g. "'https://s3.amazonaws.com/hakim-static/reveal-js/reveal-parallax-1.jpg'"

  // Parallax background size
  parallaxBackgroundSize: '', // CSS syntax, e.g. "2100px 900px"

  // Number of pixels to move the parallax background per slide
  // - Calculated automatically unless specified
  // - Set to 0 to disable movement along an axis
  parallaxBackgroundHorizontal: null,
  parallaxBackgroundVertical: null,

  // The display mode that will be used to show slides
  display: 'block'

});
```

The configuration can be updated after initialization using the `configure` method:

```javascript
// Turn autoSlide off
Reveal.configure({ autoSlide: 0 });

// Start auto-sliding every 5s
Reveal.configure({ autoSlide: 5000 });
```

### Presentation Size

All presentations have a normal size, that is, the resolution at which they are authored. The framework will automatically scale presentations uniformly based on this size to ensure that everything fits on any given display or viewport.

See below for a list of configuration options related to sizing, including default values:

```javascript
Reveal.initialize({

  // ...

  // The "normal" size of the presentation, aspect ratio will be preserved
  // when the presentation is scaled to fit different resolutions. Can be
  // specified using percentage units.
  width: 960,
  height: 700,

  // Factor of the display size that should remain empty around the content
  margin: 0.1,

  // Bounds for smallest/largest possible scale to apply to content
  minScale: 0.2,
  maxScale: 1.5

});
```

If you wish to disable this behavior and do your own scaling (e.g. using media queries), try these settings:

```javascript
Reveal.initialize({

  // ...

  width: "100%",
  height: "100%",
  margin: 0,
  minScale: 1,
  maxScale: 1
});
```

### Ready Event

A `ready` event is fired when reveal.js has loaded all non-async dependencies and is ready to start navigating. To check if reveal.js is already 'ready' you can call `Reveal.isReady()`.

```javascript
Reveal.on( 'ready', event => {
  // event.currentSlide, event.indexh, event.indexv
} );
```

Note that we also add a `.ready` class to the `.reveal` element so that you can hook into this with CSS.

### Auto-Slide

Presentations can be configured to progress through slides automatically, without any user input. To enable this you will need to tell the framework how many milliseconds it should wait between slides:

```javascript
// Slide every five seconds
Reveal.configure({
  autoSlide: 5000
});
```

When this is turned on a control element will appear that enables users to pause and resume auto-sliding. Alternatively, sliding can be paused or resumed by pressing »A« on the keyboard. Sliding is paused automatically as soon as the user starts navigating. You can disable these controls by specifying `autoSlideStoppable: false` in your reveal.js config.

You can also override the slide duration for individual slides and fragments by using the `data-autoslide` attribute:

```html
<section data-autoslide="2000">
  <p>After 2 seconds the first fragment will be shown.</p>
  <p class="fragment" data-autoslide="10000">After 10 seconds the next fragment will be shown.</p>
  <p class="fragment">Now, the fragment is displayed for 2 seconds before the next slide is shown.</p>
</section>
```

To override the method used for navigation when auto-sliding, you can specify the `autoSlideMethod` setting. To only navigate along the top layer and ignore vertical slides, set this to `Reveal.navigateRight`.

Whenever the auto-slide mode is resumed or paused the `autoslideresumed` and `autoslidepaused` events are fired.

### Keyboard Bindings

If you're unhappy with any of the default keyboard bindings you can override them using the `keyboard` config option:

```javascript
Reveal.configure({
  keyboard: {
    13: 'next', // go to the next slide when the ENTER key is pressed
    27: () => { console.log('esc') }, // do something custom when ESC is pressed
    32: null // don't do anything when SPACE is pressed (i.e. disable a reveal.js default binding)
  }
});
```

### Auto-Animate

reveal.js can automatically animate elements across slides. All you need to do is add `data-auto-animate` to two adjacent slide `<section>` elements and Auto-Animate will animate all matching elements between the two.

Here's a simple example to give you a better idea of how it can be used. The resulting animation will be the word "Magic" sliding 100px downwards.
```html
<section data-auto-animate>
  <h1>Magic</h1>
</section>
<section data-auto-animate>
  <h1 style="position: relative; top: 100px;">Magic</h1>
</section>
```

This example uses the `top` property to move the element but internally reveal.js will use a CSS transform to ensure smooth movement. This same approach to animation works with most animatable CSS properties meaning you can transition things like `position`, `font-size`, `line-height`, `color`, `background-color` and `padding`.

#### How Elements are Matched
When you navigate between two auto-animated slides we'll do our best to automatically find matching elements between the two slides. For text, we consider it a match if both the text contents and node type are identical. For images, videos and iframes we compare the `src` attribute. We also take into account the order in which the element appears in the DOM.

In situations where automatic matching is not feasible you can give the objects that you want to animate between a matching `data-id` attribute. We prioritize matching `data-id` values above our automatic matching. 

Here's an example where we've given both blocks a matching ID since automatic matching has no content to go on.

```html
<section data-auto-animate>
  <div data-id="box" style="padding: 20px; background: salmon;"></div>
</section>
<section data-auto-animate>
  <div data-id="box" style="padding: 20px; background: blue;"></div>
</section>
```

#### Animation Settings
You can override specific animation settings such as easing and duration either for the whole presentation, per-slide or individually for each animated element. The following configuration attributes can be used to change the settings for a specific slide or element:

| Attribute&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                        | Default    | Description 
| :------------------------------- | ---------: | :---------- 
| data-auto-animate-easing         | ease       | A CSS [easing function](https://developer.mozilla.org/en-US/docs/Web/CSS/easing-function).
| data-auto-animate-unmatched      | true       | Determines whether elements with no matching auto-animate target should fade in. Set to false to make them appear instantly.
| data-auto-animate-duration       | 1.0        | Animation duration in seconds.
| data-auto-animate-delay          | 0          | Animation delay in seconds (can only be set for specific elements, not at the slide level).

If you'd like to change the defaults for the whole deck, use the following config options:
```javascript
Reveal.initialize({
  autoAnimateEasing: 'ease-out',
  autoAnimateDuration: 0.8,
  autoAnimateUnmatched: false
})
```

#### API: State Attributes and Events
We add state attributes to the different elements involved in an auto-animation. These attributes can be tied into if you want to, for example, fine-tune the animation behavior with custom CSS.

Right before an auto-animation starts we add `data-auto-animate="pending"` to the slide `<section>`. At this point the upcoming slide is visible and all of the animated elements have been moved to their starting positions. Next we switch to `data-auto-animate="running"` to indicate when the elements start animating towards their final properties.

Each individual element is decorated with a `data-auto-animate-target` attribute. The value of the attribute is a unique ID for this particular animation OR "unmatched" if this element should animate as unmatched content.

Each time a presentation navigates between two auto-animated slides it dispatches the `autoanimate` event.
```javascript
Reveal.on( 'autoanimate', event => {
  // event.fromSlide, event.toSlide
} );
```

### Vertical Slide Navigation

Slides can be nested within other slides to create vertical stacks (see [Markup](#markup)). When presenting, you use the left/right arrows to step through the main (horizontal) slides. When you arrive at a vertical stack you can optionally press the up/down arrows to view the vertical slides or skip past them by pressing the right arrow. Here's an example showing a bird's-eye view of what this looks like in action:

<img src="https://static.slid.es/support/reveal.js-vertical-slides.gif" width="450">

#### Navigation Mode
You can fine tune the reveal.js navigation behavior by using the `navigationMode` config option. Note that these options are only useful for presentations that use a mix of horizontal and vertical slides. The following navigation modes are available:

| Value                         | Description |
| :---------------------------  | :---------- |
| default                       | Left/right arrow keys step between horizontal slides. Up/down arrow keys step between vertical slides. Space key steps through all slides (both horizontal and vertical). |
| linear                        | Removes the up/down arrows. Left/right arrows step through all slides (both horizontal and vertical). |
| grid                          | When this is enabled, stepping left/right from a vertical stack to an adjacent vertical stack will land you at the same vertical index.<br><br>Consider a deck with six slides ordered in two vertical stacks:<br>`1.1`&nbsp;&nbsp;&nbsp;&nbsp;`2.1`<br>`1.2`&nbsp;&nbsp;&nbsp;&nbsp;`2.2`<br>`1.3`&nbsp;&nbsp;&nbsp;&nbsp;`2.3`<br><br>If you're on slide 1.3 and navigate right, you will normally move from 1.3 -> 2.1. With navigationMode set to "grid" the same navigation takes you from 1.3 -> 2.3. |

### Touch Navigation

You can swipe to navigate through a presentation on any touch-enabled device. Horizontal swipes change between horizontal slides, vertical swipes change between vertical slides. If you wish to disable this you can set the `touch` config option to false when initializing reveal.js.

If there's some part of your content that needs to remain accessible to touch events you'll need to highlight this by adding a `data-prevent-swipe` attribute to the element. One common example where this is useful is elements that need to be scrolled.



### Plugins

**Outdated, this will be rewritten to match the 4.0 plugin API**

Plugins should register themselves with reveal.js by calling `Reveal.registerPlugin( MyPlugin )`. Registered plugins _must_ expose a unique `id` property and can optionally expose an `init` function that reveal.js will call to initialize them.

When reveal.js is booted up via `initialize()`, it will go through all registered plugins and invoke their `init` methods. If the `init` method returns a Promise, reveal.js will wait for that promise to be fulfilled before finishing the startup sequence and firing the [ready](#ready-event) event. Here’s an example of a plugin that does some asynchronous work before reveal.js can proceed:

```javascript
let MyPlugin = {
  id: ’my-plugin’,
  init: deck => {
    return new Promise( resolve => setTimeout( resolve, 3000 ) )
  }
};
Reveal.initialize({
  plugins: [ MyPlugin ]
}).then( () => {
  console.log( ’Three seconds later...’ )
} );
```

If the plugin’s init method does _not_ return a Promise, the plugin is considered ready right away and will not hold up the reveal.js startup sequence.

### Manually Registering Plugins

TBD. Describe how plugins can be registered after reveal.js is already initialized.

### Retrieving Plugins

If you want to check if a specific plugin is registered you can use the `Reveal.hasPlugin` method and pass in a plugin ID, for example: `Reveal.hasPlugin( ’my-plugin’ )`. If you want to retrieve a plugin instance you can use `Reveal.getPlugin( ’my-plugin’ )`.

### Dependencies

Reveal.js doesn’t _rely_ on any third party scripts to work but a few optional libraries are included by default. These libraries are loaded as dependencies in the order they appear, for example:

```javascript
Reveal.initialize({
  dependencies: [
    // Interpret Markdown in <section> elements
    { src: ’plugin/markdown/marked.js’, condition: () => { return !!document.querySelector( ’[data-markdown]’ ); } },
    { src: ’plugin/markdown/markdown.js’, condition: () => { return !!document.querySelector( ’[data-markdown]’ ); } },

    // Syntax highlight for <code> elements
    { src: ’plugin/highlight/highlight.js’, async: true },

    // Zoom in and out with Alt+click
    { src: ’plugin/zoom-js/zoom.js’, async: true },

    // Speaker notes
    { src: ’plugin/notes/notes.js’, async: true },

    // MathJax
    { src: ’plugin/math/math.js’, async: true }
  ]
});
```

You can add your own extensions using the same syntax. The following properties are available for each dependency object:
- **src**: Path to the script to load
- **async**: [optional] Flags if the script should load after reveal.js has started, defaults to false
- **callback**: [optional] Function to execute when the script has loaded
- **condition**: [optional] Function which must return true for the script to be loaded

You can also include dependencies which are bundled/already present on the page. To include a bundled plugin. replace the `src` property with a reference to a `plugin` instance:
- **plugin**: the plugin instance (see [Plugins](#plugins))

### API

The `Reveal` object exposes a JavaScript API for controlling navigation and reading state:

```javascript
// Navigation
Reveal.slide( indexh, indexv, indexf );
Reveal.left();
Reveal.right();
Reveal.up();
Reveal.down();
Reveal.prev();
Reveal.next();
Reveal.prevFragment();
Reveal.nextFragment();

// Randomize the order of slides
Reveal.shuffle();

// Toggle presentation states, optionally pass true/false to force on/off
Reveal.toggleOverview();
Reveal.togglePause();
Reveal.toggleAutoSlide();

// Shows a help overlay with keyboard shortcuts, optionally pass true/false
// to force on/off
Reveal.toggleHelp();

// Change a config value at runtime
Reveal.configure({ controls: true });

// Returns the present configuration options
Reveal.getConfig();

// Fetch the current scale of the presentation
Reveal.getScale();

Reveal.getComputedSlideSize(); // Returns object with width, height keys, and (scaled) presentationWidth and presentationHeight.

// Retrieves the previous and current slide elements
Reveal.getPreviousSlide();
Reveal.getCurrentSlide();

Reveal.getIndices();        // { h: 0, v: 0, f: 0 }
Reveal.getSlidePastCount();
Reveal.getProgress();       // (0 == first slide, 1 == last slide)
Reveal.getSlides();         // Array of all slides
Reveal.getTotalSlides();    // Total number of slides

// Returns an array with all horizontal/vertical slides in the deck
Reveal.getHorizontalSlides();
Reveal.getVerticalSlides();

// Checks if the presentation contains two or more
// horizontal/vertical slides
Reveal.hasHorizontalSlides();
Reveal.hasVerticalSlides();

// Returns the speaker notes for the current slide
Reveal.getSlideNotes();

// State checks
Reveal.isFirstSlide();
Reveal.isLastSlide();
Reveal.isOverview();
Reveal.isPaused();
Reveal.isAutoSliding();

// Returns the top-level DOM element
Reveal.getRevealElement(); // <div class="reveal">...</div>
```

### Custom Key Bindings

Custom key bindings can be added and removed using the following Javascript API. Custom key bindings will override the default keyboard bindings, but will in turn be overridden by the user defined bindings in the ``keyboard`` config option.

```javascript
Reveal.addKeyBinding( binding, callback );
Reveal.removeKeyBinding( keyCode );
```

For example

```javascript
// The binding parameter provides the following properties
//      keyCode: the keycode for binding to the callback
//          key: the key label to show in the help overlay
//  description: the description of the action to show in the help overlay
Reveal.addKeyBinding( { keyCode: 84, key: 'T', description: 'Start timer' }, () => {
  // start timer
} )

// The binding parameter can also be a direct keycode without providing the help description
Reveal.addKeyBinding( 82, () => {
  // reset timer
} )
```

This allows plugins to add key bindings directly to Reveal so they can

* make use of Reveal's pre-processing logic for key handling (for example, ignoring key presses when paused); and
* be included in the help overlay (optional)

### Slide Change Events

A `slidechanged` event is fired each time the slide is changed. The event object holds the index values of the current slide as well as a reference to the previous and current slide DOM nodes.

Some libraries, like MathJax (see [#226](https://github.com/hakimel/reveal.js/issues/226#issuecomment-10261609)), get confused by the transforms and display states of slides. Often times, this can be fixed by calling their update or render function from this callback.

```javascript
Reveal.on( 'slidechanged', event => {
  // event.previousSlide, event.currentSlide, event.indexh, event.indexv
} );
```

The `slidechanged` event fires instantly when the slide changes. If you'd rather invoke your event listener when the slide has finished transitioning and is fully visible, you can use the `slidetransitionend` event. The `slidetransitionend` event includes the same event data as described above.

```javascript
Reveal.on( 'slidetransitionend', event => console.log( event.currentSlide ) );
```

### Presentation State

The presentation's current state can be fetched by using the `getState` method. A state object contains all of the information required to put the presentation back as it was when `getState` was first called. Sort of like a snapshot. It's a simple object that can easily be stringified and persisted or sent over the wire.

```javascript
Reveal.slide( 1 );
// we're on slide 1

var state = Reveal.getState();

Reveal.slide( 3 );
// we're on slide 3

Reveal.setState( state );
// we're back on slide 1
```

### Slide States

If you set `data-state="somestate"` on a slide `<section>`, "somestate" will be applied as a class on the document element when that slide is opened. This allows you to apply broad style changes to the page based on the active slide.

Furthermore you can also listen to these changes in state via JavaScript:

```javascript
Reveal.on( 'somestate', () => {
  // TODO: Sprinkle magic
}, false );
```

### Slide Visibility
When preparing a presentation it can sometimes be helpful to prepare optional slides that you may or may not have time to show. This is easily done by appending a few slides at the end of the presentation, however this means that the reveal.js progress bar and slide numbering will hint that there are additional slides.

To "hide" those slides from reveal.js' numbering system you can add a `data-visibility` attribute to the slide like so `<section data-visibility="uncounted">`.

### Slide Backgrounds

Slides are contained within a limited portion of the screen by default to allow them to fit any display and scale uniformly. You can apply full page backgrounds outside of the slide area by adding a `data-background` attribute to your `<section>` elements. Four different types of backgrounds are supported: color, image, video and iframe.

#### Color Backgrounds

All CSS color formats are supported, including hex values, keywords, `rgba()` or `hsl()`.

```html
<section data-background-color="#ff0000">
  <h2>Color</h2>
</section>
```

#### Image Backgrounds

By default, background images are resized to cover the full page. Available options:

| Attribute                        | Default    | Description |
| :------------------------------- | :--------- | :---------- |
| data-background-image            |            | URL of the image to show. GIFs restart when the slide opens. |
| data-background-size             | cover      | See [background-size](https://developer.mozilla.org/docs/Web/CSS/background-size) on MDN.  |
| data-background-position         | center     | See [background-position](https://developer.mozilla.org/docs/Web/CSS/background-position) on MDN. |
| data-background-repeat           | no-repeat  | See [background-repeat](https://developer.mozilla.org/docs/Web/CSS/background-repeat) on MDN. |
| data-background-opacity          | 1          | Opacity of the background image on a 0-1 scale. 0 is transparent and 1 is fully opaque. |

```html
<section data-background-image="http://example.com/image.png">
  <h2>Image</h2>
</section>
<section data-background-image="http://example.com/image.png" data-background-size="100px" data-background-repeat="repeat">
  <h2>This background image will be sized to 100px and repeated</h2>
</section>
```

#### Video Backgrounds

Automatically plays a full size video behind the slide.

| Attribute                        | Default | Description |
| :---------------------------     | :------ | :---------- |
| data-background-video            |         | A single video source, or a comma separated list of video sources. |
| data-background-video-loop       | false   | Flags if the video should play repeatedly. |
| data-background-video-muted      | false   | Flags if the audio should be muted. |
| data-background-size             | cover   | Use `cover` for full screen and some cropping or `contain` for letterboxing. |
| data-background-opacity          | 1       | Opacity of the background video on a 0-1 scale. 0 is transparent and 1 is fully opaque. |

```html
<section data-background-video="https://s3.amazonaws.com/static.slid.es/site/homepage/v1/homepage-video-editor.mp4,https://s3.amazonaws.com/static.slid.es/site/homepage/v1/homepage-video-editor.webm" data-background-video-loop data-background-video-muted>
  <h2>Video</h2>
</section>
```

#### Iframe Backgrounds

Embeds a web page as a slide background that covers 100% of the reveal.js width and height. The iframe is in the background layer, behind your slides, and as such it's not possible to interact with it by default. To make your background interactive, you can add the `data-background-interactive` attribute.

```html
<section data-background-iframe="https://slides.com" data-background-interactive>
  <h2>Iframe</h2>
</section>
```

Iframes are lazy-loaded when they become visible. If you'd like to preload iframes ahead of time, you can append a `data-preload` attribute to the slide `<section>`. You can also enable preloading globally for all iframes using the `preloadIframes` configuration option.

#### Background Transitions

Backgrounds transition using a fade animation by default. This can be changed to a linear sliding transition by passing `backgroundTransition: 'slide'` to the `Reveal.initialize()` call. Alternatively you can set `data-background-transition` on any section with a background to override that specific transition.


### Parallax Background

If you want to use a parallax scrolling background, set the first two properties below when initializing reveal.js (the other two are optional).

```javascript
Reveal.initialize({

  // Parallax background image
  parallaxBackgroundImage: '', // e.g. "https://s3.amazonaws.com/hakim-static/reveal-js/reveal-parallax-1.jpg"

  // Parallax background size
  parallaxBackgroundSize: '', // CSS syntax, e.g. "2100px 900px" - currently only pixels are supported (don't use % or auto)

  // Number of pixels to move the parallax background per slide
  // - Calculated automatically unless specified
  // - Set to 0 to disable movement along an axis
  parallaxBackgroundHorizontal: 200,
  parallaxBackgroundVertical: 50

});
```

Make sure that the background size is much bigger than screen size to allow for some scrolling. [View example](http://revealjs.com/?parallaxBackgroundImage=https%3A%2F%2Fs3.amazonaws.com%2Fhakim-static%2Freveal-js%2Freveal-parallax-1.jpg&parallaxBackgroundSize=2100px%20900px).

### Slide Transitions

The global presentation transition is set using the `transition` config value. You can override the global transition for a specific slide by using the `data-transition` attribute:

```html
<section data-transition="zoom">
  <h2>This slide will override the presentation transition and zoom!</h2>
</section>

<section data-transition-speed="fast">
  <h2>Choose from three transition speeds: default, fast or slow!</h2>
</section>
```

You can also use different in and out transitions for the same slide:

```html
<section data-transition="slide">
    The train goes on …
</section>
<section data-transition="slide">
    and on …
</section>
<section data-transition="slide-in fade-out">
    and stops.
</section>
<section data-transition="fade-in slide-out">
    (Passengers entering and leaving)
</section>
<section data-transition="slide">
    And it starts again.
</section>
```
You can choose from `none`, `fade`, `slide`, `convex`, `concave` and `zoom`.
### Internal links

It's easy to link between slides. The first example below targets the index of another slide whereas the second targets a slide with an ID attribute (`<section id="some-slide">`):

```html
<a href="#/2/2">Link</a>
<a href="#/some-slide">Link</a>
```

You can also add relative navigation links, similar to the built in reveal.js controls, by appending one of the following classes on any element. Note that each element is automatically given an `enabled` class when it's a valid navigation route based on the current slide.

```html
<a href="#" class="navigate-left">
<a href="#" class="navigate-right">
<a href="#" class="navigate-up">
<a href="#" class="navigate-down">
<a href="#" class="navigate-prev"> <!-- Previous vertical or horizontal slide -->
<a href="#" class="navigate-next"> <!-- Next vertical or horizontal slide -->
```

### Fragments

Fragments are used to highlight individual elements on a slide. Every element with the class `fragment` will be stepped through before moving on to the next slide. Here's an example: http://revealjs.com/#/fragments

The default fragment style is to start out invisible and fade in. This style can be changed by appending a different class to the fragment:

```html
<section>
  <p class="fragment grow">grow</p>
  <p class="fragment shrink">shrink</p>
  <p class="fragment strike">strike</p>
  <p class="fragment fade-out">fade-out</p>
  <p class="fragment fade-up">fade-up (also down, left and right!)</p>
  <p class="fragment fade-in-then-out">fades in, then out when we move to the next step</p>
  <p class="fragment fade-in-then-semi-out">fades in, then obfuscate when we move to the next step</p>
  <p class="fragment highlight-current-blue">blue only once</p>
  <p class="fragment highlight-red">highlight-red</p>
  <p class="fragment highlight-green">highlight-green</p>
  <p class="fragment highlight-blue">highlight-blue</p>
</section>
```

Multiple fragments can be applied to the same element sequentially by wrapping it, this will fade in the text on the first step and fade it back out on the second.

```html
<section>
  <span class="fragment fade-in">
    <span class="fragment fade-out">I'll fade in, then out</span>
  </span>
</section>
```

The display order of fragments can be controlled using the `data-fragment-index` attribute.

```html
<section>
  <p class="fragment" data-fragment-index="3">Appears last</p>
  <p class="fragment" data-fragment-index="1">Appears first</p>
  <p class="fragment" data-fragment-index="2">Appears second</p>
</section>
```

### Fragment events

When a slide fragment is either shown or hidden reveal.js will dispatch an event.

Some libraries, like MathJax (see #505), get confused by the initially hidden fragment elements. Often times this can be fixed by calling their update or render function from this callback.

```javascript
Reveal.on( 'fragmentshown', event => {
  // event.fragment = the fragment DOM element
} );
Reveal.on( 'fragmenthidden', event => {
  // event.fragment = the fragment DOM element
} );
```

### Code Syntax Highlighting

By default, Reveal is configured with [highlight.js](https://highlightjs.org/) for code syntax highlighting. To enable syntax highlighting, you'll have to load the highlight plugin ([plugin/highlight/highlight.js](plugin/highlight/highlight.js)) and a highlight.js CSS theme (Reveal comes packaged with the Monokai themes: [lib/css/monokai.css](lib/css/monokai.css)).

```javascript
Reveal.initialize({
  // More info https://github.com/hakimel/reveal.js#dependencies
  dependencies: [
    { src: 'plugin/highlight/highlight.js', async: true },
  ]
});
```

Below is an example with clojure code that will be syntax highlighted. When the `data-trim` attribute is present, surrounding whitespace is automatically removed.  HTML will be escaped by default. To avoid this, for example if you are using `<mark>` to call out a line of code, add the `data-noescape` attribute to the `<code>` element.

```html
<section>
  <pre><code data-trim data-noescape>
(def lazy-fib
  (concat
   [0 1]
   <mark>((fn rfib [a b]</mark>
        (lazy-cons (+ a b) (rfib b (+ a b)))) 0 1)))
  </code></pre>
</section>
```

#### Line Numbers & Highlights

To enable line numbers, add `data-line-numbers` to your `<code>` tags. If you want to highlight specific lines you can provide a comma separated list of line numbers using the same attribute. For example, in the following example lines 4 and 8-11 are highlighted:

```html
<pre><code class="hljs" data-line-numbers="4,8-11">
import React, { useState } from 'react';
 
function Example() {
  const [count, setCount] = useState(0);
 
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
</code></pre>
```

<img width="300" alt="line-numbers" src="https://user-images.githubusercontent.com/629429/55332077-eb3c4780-5494-11e9-8854-ba33cd0fa740.png">

#### Step-by-step Highlights

You can step through multiple code highlights on the same code block. Delimit each of your highlight steps with the `|` character. For example `data-line-numbers="1|2-3|4,6-10"` will produce three steps. It will start by highlighting line 1, next step is lines 2-3, and finally line 4 and 6 through 10.



### Slide number

If you would like to display the page number of the current slide you can do so using the `slideNumber` and `showSlideNumber` configuration values.

```javascript
// Shows the slide number using default formatting
Reveal.configure({ slideNumber: true });

// Slide number formatting can be configured using these variables:
//  "h.v":  horizontal . vertical slide number (default)
//  "h/v":  horizontal / vertical slide number
//    "c":  flattened slide number
//  "c/t":  flattened slide number / total slides
Reveal.configure({ slideNumber: 'c/t' });

// You can provide a function to fully customize the number:
Reveal.configure({ slideNumber: slide => {
    // Ignore numbering of vertical slides
    return [ Reveal.getIndices( slide ).h ];
}});

// Control which views the slide number displays on using the "showSlideNumber" value:
//     "all": show on all views (default)
// "speaker": only show slide numbers on speaker notes view
//   "print": only show slide numbers when printing to PDF
Reveal.configure({ showSlideNumber: 'speaker' });
```

### Overview mode

Press »ESC« or »O« keys to toggle the overview mode on and off. While you're in this mode, you can still navigate between slides,
as if you were at 1,000 feet above your presentation. The overview mode comes with a few API hooks:

```javascript
Reveal.on( 'overviewshown', event => { /* ... */ } );
Reveal.on( 'overviewhidden', event => { /* ... */ } );

// Toggle the overview mode programmatically
Reveal.toggleOverview();
```

### Fullscreen mode

Just press »F« on your keyboard to show your presentation in fullscreen mode. Press the »ESC« key to exit fullscreen mode.

### Embedded media

Add `data-autoplay` to your media element if you want it to automatically start playing when the slide is shown:

```html
<video data-autoplay src="http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4"></video>
```

If you want to enable or disable autoplay globally, for all embedded media, you can use the `autoPlayMedia` configuration option. If you set this to `true` ALL media will autoplay regardless of individual `data-autoplay` attributes. If you initialize with `autoPlayMedia: false` NO media will autoplay.

Note that embedded HTML5 `<video>`/`<audio>` and YouTube/Vimeo iframes are automatically paused when you navigate away from a slide. This can be disabled by decorating your element with a `data-ignore` attribute.

### Embedded iframes

reveal.js automatically pushes two [post messages](https://developer.mozilla.org/en-US/docs/Web/API/Window.postMessage) to embedded iframes. `slide:start` when the slide containing the iframe is made visible and `slide:stop` when it is hidden.

### Stretching elements

Sometimes it's desirable to have an element, like an image or video, stretch to consume as much space as possible within a given slide. This can be done by adding the `.stretch` class to an element as seen below:

```html
<section>
  <h2>This video will use up the remaining space on the slide</h2>
    <video class="stretch" src="http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4"></video>
</section>
```

Limitations:
- Only direct descendants of a slide section can be stretched
- Only one descendant per slide section can be stretched

### Resize Event

When reveal.js changes the scale of the slides it fires a resize event. You can subscribe to the event to resize your elements accordingly.

```javascript
Reveal.on( 'resize', event => {
  // event.scale, event.oldScale, event.size
} );
```

### postMessage API

The framework has a built-in postMessage API that can be used when communicating with a presentation inside of another window. Here's an example showing how you'd make a reveal.js instance in the given window proceed to slide 2:

```javascript
<window>.postMessage( JSON.stringify({ method: 'slide', args: [ 2 ] }), '*' );
```

#### postMessage Events

When reveal.js runs inside of an iframe it can optionally bubble all of its events to the parent. Bubbled events are stringified JSON with three fields: namespace, eventName and state. Here's how you subscribe to them from the parent window:

```javascript
window.addEventListener( 'message', event => {
  var data = JSON.parse( event.data );
  if( data.namespace === 'reveal' && data.eventName === 'slidechanged' ) {
    // Slide changed, see data.state for slide number
  }
} );
```

#### postMessage Callbacks

When you call any method via the postMessage API, reveal.js will dispatch a message with the return value. This is done so that you can call a getter method and see what the result is. Check out this example:

```javascript
<revealWindow>.postMessage( JSON.stringify({ method: 'getTotalSlides' }), '*' );

window.addEventListener( 'message', event => {
  var data = JSON.parse( event.data );
  // `data.method`` is the method that we invoked
  if( data.namespace === 'reveal' && data.eventName === 'callback' && data.method === 'getTotalSlides' ) {
    data.result // = the total number of slides
  }
} );
```

#### Turning postMessage on/off

This cross-window messaging can be toggled on or off using configuration flags. These are the default values.

```javascript
Reveal.initialize({
  // ...

  // Exposes the reveal.js API through window.postMessage
  postMessage: true,

  // Dispatches all reveal.js events to the parent window through postMessage
  postMessageEvents: false
});
```



## PDF Export

Presentations can be exported to PDF via a special print stylesheet. This feature requires that you use [Google Chrome](http://google.com/chrome) or [Chromium](https://www.chromium.org/Home) and to be serving the presentation from a web server.
Here's an example of an exported presentation that's been uploaded to SlideShare: http://www.slideshare.net/hakimel/revealjs-300.

### Separate pages for fragments
[Fragments](#fragments) are printed on separate slides by default. Meaning if you have a slide with three fragment steps, it will generate three separate slides where the fragments appear incrementally.

If you prefer printing all fragments in their visible states on the same slide you can set the `pdfSeparateFragments` config option to false.

### Page size

Export dimensions are inferred from the configured [presentation size](#presentation-size). Slides that are too tall to fit within a single page will expand onto multiple pages. You can limit how many pages a slide may expand onto using the `pdfMaxPagesPerSlide` config option, for example `Reveal.configure({ pdfMaxPagesPerSlide: 1 })` ensures that no slide ever grows to more than one printed page.

### Instructions

1. Open your presentation with `print-pdf` included in the query string i.e. http://localhost:8000/?print-pdf. You can test this with [revealjs.com?print-pdf](http://revealjs.com?print-pdf).
  * If you want to include [speaker notes](#speaker-notes) in your export, you can append `showNotes=true` to the query string: http://localhost:8000/?print-pdf&showNotes=true
1. Open the in-browser print dialog (CTRL/CMD+P).
1. Change the **Destination** setting to **Save as PDF**.
1. Change the **Layout** to **Landscape**.
1. Change the **Margins** to **None**.
1. Enable the **Background graphics** option.
1. Click **Save**.

![Chrome Print Settings](https://s3.amazonaws.com/hakim-static/reveal-js/pdf-print-settings-2.png)

Alternatively you can use the [decktape](https://github.com/astefanutti/decktape) project.


## Theming

The framework comes with a few different themes included:

- black: Black background, white text, blue links (default theme)
- white: White background, black text, blue links
- league: Gray background, white text, blue links (default theme for reveal.js < 3.0.0)
- beige: Beige background, dark text, brown links
- sky: Blue background, thin dark text, blue links
- night: Black background, thick white text, orange links
- serif: Cappuccino background, gray text, brown links
- simple: White background, black text, blue links
- solarized: Cream-colored background, dark green text, blue links

Each theme is available as a separate stylesheet. To change theme you will need to replace **black** below with your desired theme name in index.html:

```html
<link rel="stylesheet" href="css/theme/black.css" id="theme">
```

If you want to add a theme of your own see the instructions here: [/css/theme/README.md](https://github.com/hakimel/reveal.js/blob/master/css/theme/README.md).

All theme variables are exposed as CSS custom properties in the pseudo-class `:root`. See [the list of exposed variables](https://github.com/hakimel/reveal.js/blob/master/css/theme/template/exposer.scss).

## Speaker Notes

reveal.js comes with a speaker notes plugin which can be used to present per-slide notes in a separate browser window. The notes window also gives you a preview of the next upcoming slide so it may be helpful even if you haven't written any notes. Press the »S« key on your keyboard to open the notes window.

A speaker timer starts as soon as the speaker view is opened. You can reset it to 00:00:00 at any time by simply clicking/tapping on it.

Notes are defined by appending an `<aside>` element to a slide as seen below. You can add the `data-markdown` attribute to the aside element if you prefer writing notes using Markdown.

Alternatively you can add your notes in a `data-notes` attribute on the slide. Like `<section data-notes="Something important"></section>`.

When used locally, this feature requires that reveal.js [runs from a local web server](#full-setup).

```html
<section>
  <h2>Some Slide</h2>

  <aside class="notes">
    Oh hey, these are some notes. They'll be hidden in your presentation, but you can see them if you open the speaker notes window (hit »S« on your keyboard).
  </aside>
</section>
```

If you're using the external Markdown plugin, you can add notes with the help of a special delimiter:

```html
<section data-markdown="example.md" data-separator="^\n\n\n" data-separator-vertical="^\n\n" data-separator-notes="^Note:"></section>

# Title
## Sub-title

Here is some content...

Note:
This will only display in the notes window.
```

#### Share and Print Speaker Notes

Notes are only visible to the speaker inside of the speaker view. If you wish to share your notes with others you can initialize reveal.js with the `showNotes` configuration value set to `true`. Notes will appear along the bottom of the presentations.

When `showNotes` is enabled notes are also included when you [export to PDF](https://github.com/hakimel/reveal.js#pdf-export). By default, notes are printed in a box on top of the slide. If you'd rather print them on a separate page, after the slide, set `showNotes: "separate-page"`.

#### Speaker notes clock and timers

The speaker notes window will also show:

- Time elapsed since the beginning of the presentation.  If you hover the mouse above this section, a timer reset button will appear.
- Current wall-clock time
- (Optionally) a pacing timer which indicates whether the current pace of the presentation is on track for the right timing (shown in green), and if not, whether the presenter should speed up (shown in red) or has the luxury of slowing down (blue).

The pacing timer can be enabled by configuring the `defaultTiming` parameter in the `Reveal` configuration block, which specifies the number of seconds per slide.  120 can be a reasonable rule of thumb.  Alternatively, you can enable the timer by setting `totalTime`, which sets the total length of your presentation (also in seconds).  If both values are specified, `totalTime` wins and `defaultTiming` is ignored.  Regardless of the baseline timing method, timings can also be given per slide `<section>` by setting the `data-timing` attribute (again, in seconds).


## Server Side Speaker Notes

In some cases it can be desirable to run notes on a separate device from the one you're presenting on. The Node.js-based notes plugin lets you do this using the same note definitions as its client side counterpart. See <https://github.com/reveal/notes-server>.


## Multiplexing

The multiplex plugin allows your audience to follow the slides of the presentation you are controlling on their own phone, tablet or laptop. As of 4.0.0 this plugin has moved to its own repo at <https://github.com/reveal/multiplex>.


## MathJax

If you want to display math equations in your presentation you can easily do so by including this plugin. The plugin is a very thin wrapper around the [MathJax](http://www.mathjax.org/) library. To use it you'll need to include it as a reveal.js dependency, [find our more about dependencies here](#dependencies).

The plugin defaults to using [LaTeX](https://en.wikipedia.org/wiki/LaTeX) but that can be adjusted through the `math` configuration object. Note that MathJax is loaded from a remote server. If you want to use it offline you'll need to download a copy of the library and adjust the `mathjax` configuration value.

Below is an example of how the plugin can be configured. If you don't intend to change these values you do not need to include the `math` config object at all.

```js
Reveal.initialize({
  // other options ...

  math: {
    mathjax: 'https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js',
    config: 'TeX-AMS_HTML-full', // See http://docs.mathjax.org/en/latest/config-files.html
    // pass other options into `MathJax.Hub.Config()`
    TeX: { Macros: { RR: "{\\bf R}" } }
  },

  dependencies: [
    { src: 'plugin/math/math.js', async: true }
  ]
});
```

Read MathJax's documentation if you need [HTTPS delivery](http://docs.mathjax.org/en/latest/start.html#secure-access-to-the-cdn) or serving of [specific versions](http://docs.mathjax.org/en/latest/configuration.html#loading-mathjax-from-the-cdn) for stability.

#### MathJax in Markdown
If you want to include math inside of a presentation written in Markdown you need to wrap the formula in backticks. This prevents syntax conflicts between LaTeX and Markdown. For example:

```
`$$ J(\theta_0,\theta_1) = \sum_{i=0} $$`
```

## License

MIT licensed

Copyright (C) 2020 Hakim El Hattab, http://hakim.se