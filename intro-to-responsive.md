# Intro to Responsive and Mobile-First Layouts

_with Leif and Devon_

## Overview

* What is a responsive layout?
* What does "mobile first" mean?
* CSS techniques for responsive layouts
* Common layout patterns
* Testing responsive layouts
* Expanded topics and questions
* Resources for creating responsive layouts

## Responsive layouts

In a nutshell, the idea of a responsive layout is to _create a web UI that works regardless of the browser or device you're using_.

Implementing a responsive layout requires using **CSS** and sometimes **Javascript** to make a web page display in a way that is appropriate to the dimensions of a browser window or a device screen.

## Mobile-first philosophy

### Mobile versus desktop

When "mobile" became a thing, big companies frequently had completely separate mobile and desktop sites, where the mobile site had severely limited functionality and included lots of links to "See Full Site" or "See Desktop Site," which frequently was fixed width and not at all optimized for a small and/or touch device. The implication was that you should be using a "real" computer to do the thing you were trying to do on your phone.

### Mobile-first thinking and implementation

Mobile-first philosophy is based on the idea that we shouldn't start at the desktop and work our way down. Instead, we should start with design and interaction concepts that work on small screens, then use **progressive enhancement** to add more assets, larger media, more complex layouts, and (maybe) additional functionality to larger screens and devices.

Mobile-first means having _a core set of features and functionality that work on a phone, and a tablet, and also on a desktop computer_, instead of a core set of features that work on a desktop computer and are stripped down to barely work on a phone.

As an added bonus, sites that are conceptualized in a mobile-first way are also typically:

* content-focused
* easier to make accessibile
* SEO-friendly

## CSS techniques for responsive layouts

### Percentage-based container widths

Implementing a responsive layout usually means using percentage-based widths for some or all container elements, instead of pixel-based widths.

For example, this CSS:

    #column1 { width: 660px; }
    #column2 { width: 300px; }

could be used to give you a two-column layout that always has columns of 660px and 300px wide, to create ye olde canonical 960px-wide layout.

Alternately:

    #column1 { width: 70%; }
    #column2 { width: 30%; }

could be used to give you a two-column layout where the columns fluidly change based on the size of the screen.

### Using `box-sizing` to simplify container sizes

To reduce headaches related to how much space things take up on the page, you can use the CSS `box-sizing` property to simplify your container sizes.

By default, elements have a `box-sizing` value of "content-box," which makes the content of a container set its default width and height. Once you add padding or border widths, your container can grow beyond its prescribed size and make for wonky layouts.

Changing "content-box" to "border-box" in your CSS makes it so that the outer edge of your container border becomes the prescribed width and height of your container.

### Using `@media` to create breakpoints

The closest thing we have to a magic wand for truly responsive layouts is using **media features** and **breakpoints** to change layouts on different devices.

These can go in your regular stylesheet like so:

    @media all (max-width: 500px) {
        /* Your styles for layouts that are 500px wide or less */
    }

or like so:

    @media all (min-width: 760px) and (max-width: 1024px) {
        /* Your styles for layouts that are a minimum of 760px wide */
        /* and a maximum of 1024px wide */
    }

You can mix and match min-width and max-width (and some other options) to make **`@media` queries**, creating breakpoints along which your layout (or any other CSS) changes.

### Using single or multiple stylesheets

Sometimes, to strictly separate you layout and other styles for a bigger project, you might create  separate stylesheet or stylesheets just to handle your different breakpoints For example, Bootstrap has a stylesheet for its main color and typographic styles and a different one for its responsive layouts.

You could link to your different stylesheets instead of using `@media` queries in your single stylesheet like so:

    <link href="css/styles.css" rel="stylesheet">
    <link href="css/mobile.css" media="screen and (max-width: 480px)" rel="stylesheet">

## Common layout patterns

Usually, sites won't have more than two or three columns, unless they're using a grid layout of some kind.

As a result, there are only a few common responsive layouts, which mix and match columns of fixed and fluid widths:

* Fixed / fluid
* Fixed / fluid / fixed
* Fluid / fluid
* Etc.

## Testing responsive layouts

Ways to test your responsive layout include:

* **On your target device:** The best way to test responsive layouts is to test them on the various devices you're targeting, if you have them at your disposal.*
* **Using iOS Simulator:** You can also use the iOS Simulator build into XCode (which you probably have on your Mac already). The iOS Simulator lets you visit a URL in Mobile Safari in a simulated version of an iPhone or iPad, at various orientations.
* **In your desktop browser:** Depending how you're doing your `@media` queries, you may be able to just test your layout in your browser by resizing the window.

*Testing on an actual physical device has the added benefit of letting you use a cool feature built into Web Inspector: You can use Chrome and Safari on your Mac to see the Web Inspector output for Android and iOS devices, respectively!

## Expanded topics and questions

### Is there a master list of device breakpoints?

[Here is a table of the display specs for all existing iOS devices.](http://en.wikipedia.org/wiki/List_of_iOS_devices#Display)

[Here is a table of specs for all existing Windows 8 devices.](http://en.wikipedia.org/wiki/List_of_Windows_Phone_8_devices#Windows_Phone_8.0)

[Here is a diagram of approximately all the Android devices that were known in the wild in July 2013.](http://opensignal.com/reports/fragmentation-2013/)

So...no. :(

### What are some other ways to use media features?

The `width` media feature is easiest to apply for responsive layouts, but there are lots of others:

* `device-width` and `device-height` are based on the actual device dimensions
* `orientation` can change the layout depending on if a device is being held in portrait or landscape
* `aspect-ratio` can change the layout based on the aspect ratio of a browser (like 4:3 or 16:9, for example)
* `device-aspect-ratio` can change the layout based on teh aspect ratio of the actual device screen
* `resolution` and `device-pixel-ratio` can be used to serve hi-res background graphics and such to retina-type devices

And more!
 
### What's a grid system and when should I use one?

Grid systems use very granular columns widths, usually up to 12 columns, to create really complex multi-column layouts. [Bootstrap has one for example.](http://getbootstrap.com/css/#grid)

Like separate stylesheets, grid systems can sometimes be overkill, and can lead to very table-layout-like thinking.

Usually, focusing on breakpoints and a mobile-first mindset will prevent you from needing a really complex grid framework. However, sometimes designers like to use them for creating mockups, so they can be good to implement if it means easy adaptation of designs.

### What is Adaptive Images?

Adaptive Images is a server-side plugin that is designed to work with HTML and Javascript to serve device-appropriate media to different devices. [It's really cool!](https://github.com/mattwilcox/Adaptive-Images)

The result is that you can create media-heavy sites that send smaller, lighter images to phones and larger, higher-resolution images to desktop devices with retina screens.

### What are polyfills?

In addition to making complex websites load on phones while people wait for their coffee, a lot of our current struggle as front-end web devs is now:

* Making _older browsers_ respect (or gracefully ignore) new and shiny HTML5 and CSS3/4 techniques
* Making _browsers in general_ behave as we expect them to when we try our new and shiny HTML5 and CSS3/4 techniques

To do these things, we often use two groups of tools together:

* **Detection** scripts that detect what a given browser is capable of
* **Polyfill** scripts that fill in HTML5 and CSS3/4 functionality (or make it fail gracefully) for those browsers

## Resources

### Techniques and tools

* [Can I Use...](http://caniuse.com/): cross-browser compatability tables for modern front-end web development techniques
* [iOS Simulator User Guide](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/Introduction/Introduction.html): A guide to using the iPad and iPhone simulator built into XCode, including to test websites in Mobile Safari
* [HTML5shiv](https://code.google.com/p/html5shiv/): a Javascript library for teaching old IE browsers how to love
* [Media query features and specs](http://www.w3.org/TR/css3-mediaqueries/): W3C spec for media queries, and examples of each
* [Modernizr](http://modernizr.com/): a Javascript library for detecting HTML5 and CSS3/4 support in browsers
* [Selectivizr](http://selectivizr.com/): a Javascript library for teaching CSS3/4 support to older IE browsers
* [HTML5 Cross Browser Polyfills](https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-Browser-Polyfills): a master list of detection and polyfill scripts and tools

### Responsive origins and history

* [One web, by Jeremy Keith](http://adactio.com/journal/1716/)
* [Resposive Web Design, by Ethan Marcotte](http://alistapart.com/article/responsive-web-design)
