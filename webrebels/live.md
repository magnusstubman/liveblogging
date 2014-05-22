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


