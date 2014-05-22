# WebRebels 2014 - day 1

Change from last year:
* @janl is introducing presenters
* questions for the speakers should be posted on twitter marked #webrebels

## No man is an APIsland - Jed Schmidt - @jedschmidt

works at UNIQLO, 140byt.ex, brooklynjs.com 
coiner of "manburger icon"

libraries frameworks buildtools and compilers

- the present
- the future
- one weird trick


### the present

mosaic - first browser that gained traction - first browser that supported HTML
then came NetScape with JavaScript
Libraries started to evolve.. dojo, prototype,. adding to the DOM api
And then, jQuery -  wrapping the DOM, instead of adding to it.

trend: moving away from the DOM - talking indirectly to the DOM through frameworks that knows how to touch it as little as possible

### Build tools
tool chain getting thicker and thicker..

traceur-compiler: write ES6, compiles to ES5

moral : the layer of abstraction between you and what happens in the browser is getting thicker and thicker

asm.js compile javascript apps into a low level subset of javascript, which performs insanely well
ref . the birth and death of javascript presentation @ destroyallsoftware.com

APIs are becomming more declarative

### the future

underscorejs - fixes alot of problems during runtime
Not good enough.. big dependency..

Author of underscorejs created coffeescript, which included all the sweetness from underscorejs
Same problem solved at the language level.

Same guy is now working on implementing one language which combines both js/css/html * mind blown *

Deprecate your javascript - markup, style and code in one language domo-js.com (written by the presenter)

with libraries you call them
with frameworks you write code and they call you
Why don't we just compile both js/html/css into one app? instead of compiling the three in silos

"i want a virual DOM, that targets a performant subset of the DOM"

"I want more declarative, more cooperative""

### One Weird trick

Demo

"what's the most declarative app we can possibly write?"

"Lets use virtual DOMs as our asm.dom"

cooking -> human productivityl  (the brain was developed when we started cooking our food instead of eating it raw)

compiling -> developer productivity


# Git-it, Share it - Jessica Lord  - @jllord


- Why git-it
- building git-it
- git-it and github

## WHy git-it

Its hard to learn git

Hosting community hack nights - git and github is not straight forward
"Leave with your first pull request, shiny green contribution squares"

nodeconf
ref. nodeschool.io


### git-it 
https://github.com/jlord/git-it

a terminal app for learning git and the github workflow

When you finish git-it, your name gets shown on 


### NUX team
designers, developers, user experience

"How can github.com be easier, better for new users?"

## Rebel and Evolve: Moving beyond point-and-click - Anette Bergo @anettebgo

Ubuquitous web - technology accessible for anyone, anywhere anytime

step 1: responsible web design
progressive enhancement - graceful degradation

### Alternative to mouse interaction

#### keyboard
Shortcuts, How may webdevelopers create shortcuts for our webapps? It's awesome! Do it!

#### touch
1 touch event? People have 10 fingers. We should support 10 sources of touch events

Device motion - use shaky gestures, device orientation - tells you something about what environment the user is in - you can respond to that.

I want to be able to use a gamepad to access webapps - I dont want to use the analogue stick to move a pointer around on the screen to click on links.
Demo: guitarheros drums to access marketplace.com "natively"

Moral: use action buttons to trigger specific events

#### visual interaction
Gestues through webcam to navigate websites - swipe back/forward

#### Audio interaction
e.g. google search with speach
... some security issues. if you enable microphone once in chrome, all subdomains will forever have access.

The browser can also taclk back - web speech API

    var u = new SpeechSynthesisUtterance();
    u.text = "Hello web rebels!";
    speechSynthesis.speak(u);

Make your webapp offer to read the text for the user

swipe, play, tilt, shake, wave, punch, touch, type listen, press, click, speak <- greatly enhancess accessability

You can't dictate how users are going to interact with your site. We are the people who decide which direction the web is gonna go in. 
Be boring about it - dont do big exciting things. We build boring sites for boring companies who want boring designs. Just grab a couple of hours and add one interesting features to one of those boring sites. DOnt try to build massive beautiful apps. We dont get to do that.

We get to make things a little bit better. The audience is not the webrebels audience. So be boring.


## Getting touchy - an introduction to touch and pointer events - Patrick H. Lauke - @patrick_h_lauke

mostly touch screen based stuff in this talk. Speaker used to work for Opera.

Slides will go online.

"How do i know if my site is touch compatible?" You don't need to test it.
touch screen devices are mapped to classic mouse events.
This emulation works but is limiting/problematic.

### Spec

Apple "invented" touch events, adopted by chrome/firefox/opera
www.w3.org/TR/touch-events

touchstart
touchmove
touchend
touchcancel
~~touchenter~~ <- not part of the spec
~~touchleave~~ <- not part of the spec

(See slides for tap sequences)
### delayed event dispatch

When listening on click evnets, and the user taps, theres usually around 300ms of delay.
mousemove is only emulated when i tap and release. There is only one mousemove event sent when i move my finger around (upon release).

Why the delay? - if the browser didnt wait then the browser had no way of knowing if it was a single/double tap

#### When does the delay happen?
touchstart/touchmove, touchend -- 300ms delay --  

#### How can i make my app feel responsive with the delay?
Naive response: react before the 300ms delay.
touchstart for an "immediate" control. fires after finger lifted

### mousemove not tracking

mouse evnets only fired for single-finger tap. so if you use multi fingers then no click events are fired.
If i move my finger too much, then the touch event is not registered as a click event.

All browsers have small variations in the event sequence

solution: double up event handing, listen to mousemove and touchmove.

### feature detection
interlude: simple feature detection in browser

Hybrid devices: keyboard, trackpad, touchscreen
Users switch between touchscreen and mouse/keyboard

dont think
touch OR mouse OR keyboard.

Think:
touch AND mouse AND keyboard.

Solution: double up your event listeners
Use e.preventDefualt() to stop same "event" to be fired multiple times.
BEWARE: preventDefualt() kills scrolling, pinch/zoom etc.. So careful!

Browsers are working to remove 300ms delay, becuase it has been the biggest problem in the mobile space. Browsers are aware of that.
Especially when the page is not zoomable. So no need to wait.
meta user-scalable=no removes the delay in firefox/chrome

### Accessibility

"this page cant zoom" - you are killing people with reading issues.
If the user wants to zoom, let them zoom.

Some browsers have "force enable zoom" which solves the problem.

### Don't forget mouse/keyboard!
working example: bradfrostweb.com/demo/mobile-first/

### Warning
touchmove first... alot!
do minimum on each touchmove .. thousands of events happening. 

### Stop at single point? multitouch

iOS/iPAD preventDefualt() cant override 4-finger gestures. Anything above 3 fingers. you can't do in your app.. iOS will try to switch to another app

#### multi touch gestures - purely iOS stuff

gesturestart
gesturechange
gestureend

If your only targeting iOS, stay away from it.

Old devices does not support multitouch devices.
