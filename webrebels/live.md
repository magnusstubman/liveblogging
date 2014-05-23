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
Slides: slideshare.net/redux

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

### What about Internet Explorer?

One browser that didnt implement touch events - internet explorer.
up to IE9, only mouse events

#### Pointer model - unifying touch and mouse [...]
Pointer events - actually not that bad
Growing support.. w3 spec

Chromium are adding pointer events
Mozilla, same thing
Apple is not implementing it.

(see slides for pointer event sequence)

Pointer events extend mouse events

feature detection:

    if (window.PointerEvent) {
      // do stuff
    }

How many points does the hardware support?

    if (navigator.maxTouchPoints > 0) {
      // do stuff 
    }

## # process.env.NODE_ENV === 'PRODUCTION' for all your "webscale" apps! - Nuno Job - @dscape

How to make your nodejs app production ready.

works for YLD

Catroulette - cat vs humans - only cuteness comes out of it

### node/npm is super powerful - and therefore scary to put into production

Is it truly web-scale sauce?

How can i support this thing in production and avoid disaster?

apms: newrelic, strongops, github.com/lloyd/node-toobusy

massive scale: apms hurt your performance

### What to look for
basics: cpu, mem, disk
what code paths are the slowest?
is the event loop blocked? for how long? blocked why?
How many requests are you handling? normal? low?
what are you connection pool size? Adjust and re-run tests
memory leak?
database latency?
other services?

cpu bound? Use flame graphs (d-trace)

Insert raygun to get uncaught exceptions

## Transforming WebSockets - Arnout Kazemier @3rdEden
lead engeneer at nodejitsu

Major browsers are supporting the latest RFC of websockets:

* chrome 20
* firefox 12
* opera 12.1
* safari 6
* IE 10

Bi-directional
supports binary

Thats it

### the parts that nobody told you

"auto proxy discovery" in os x can fully crash your browser

iOS bug: writing to a closed websocket - fully crashes browser
Workaround: add setTImeout when you start writing to the socket, but only for iOS.

Pressing ESC in Firefox closes the WebSocket connection - makes no sense when the page is fully loaded.
Workaround: capturing the ESC event and just preventDefault() on body. - fixed in firefox 20

Firefox can create ghost connection when you connect during ws.onclose. Will stay alive forever, until you completely shutdown firefox. closing tab doesnt work.

Don't use self signed SSL certificates, blocked on firefox/safari, not for development and not in production.

4G, 3G, LTE mobile providers have reverse proxies - websockets doesnt work.
Workaround: use secure connections to block out reverse proxies

Virus scanners such as AVG block websockets

user, network and server firewalls block WebSockets.

Load balancers dont understand and block WebSockets
workaround: use load balancer in TCP mode <- not optimal

### What if we could fix all this...

Use framework? No!

ws - github.com/einaros/ws/

socket.io - dont use it in production - use it for demos - full of bugs - nobody gives a shit about it anymore

engine.io - Better than socket.io - not well battle tested yet - no message order guarantee - support multiple transports, cross domain, upgrade instead of downgrade, works behind firewalls & virusscanners
github.com/learnboost/engine.io

browserchannel - not cross domain - no websocket support - coffeescript on the server - multiple transports, client maintained by google , message order guaranteed, works behind firewalls & virusscanners

sockjs - poor error handling, no error handler, no query string allowed for connect, more coffeescript, connection delay with firewalls, pooly maintained, last update 2 years ago. New maintainer now? perhaps better, cross domain, multiple transports (tons of them)

different use cases and APIs
Changing product specs == rewrite application

### What if we could change this too...

Primus.io - wraps and improve populaire real-time frameworks. so you can focus on building apps.

#### Community
Growing steady
Everything can be extended.
Reached 1000 stars on github
5 members
Promising.

1 line of code to switch between all these different frameworks <- awesome!
    #primus on irc.freenode.net

#### bigpipe.ie - released a week ago
wrapping engine to be more useful for developers

Use primus if you want to include real time functionality in your framework
So primus is aimed at module and framework authors

#### Stability

Primus makes the frameworks more stable because they are wrapped and messages are slightly modified to avoid bugs in the frameworks

fully stream compatible, 

Primus enables transformation of messages

Reconnect - one if the vital things when building realtime apps. Remember to do a randomize exponential backoff such that all disconnected clients doesnt DDoS your server if everyone is disconnected simulatiously. Primus supports this.

Broadcasting - primus can broadcast messages to all connected clients

Primus also has a node client.

Primus supports plugins and middleware - makes keeping the core light easy

## BitTorrent, Streams and JavaScript - Mathias Buus - @mafintosh

1. What is bitTorrent
2. BitTorrent streaming
3. Mad science!

### BitTorrent

[Problems with scaling client->server downloads are explained]

[basic idea bitTorrent is explained]

[Problems with having a central torrent server is explained, DHT (distributed hash tables) are explained]

DHT tracking: https://dsn.km.kit.edu/english/2936.php  - 10 000 000 nodes at any time

Summary: bittorrent + DHT is awesome for sharing content

### Node

What the speaker likes about Node:
- async
- community
- npm
- Streams are a first class citizen

### NODE.JS STREAMS + BITTORRENT = <3 ?
### REALTIME + NODE.JS STREAMS + BITTORRENT = <3

Risk of high latency ==> does not seem realtime

Solution: fetch same piece from multiple peers to avoid one peer choking/being slow

Keep track of slow peers, and use them to fetch less important pieces.
Use high value peers to fetch important (the first) pieces.

If a fast peer becomes slow swap him for another peer

Wastes a little bandwidth, but will probably be fine.

Module that demoes this: torrent-stream


Demo - torrent-stream is demoe

Torrent-stream + vlc = <3 <3 <3 <3 ??

Peerflix!
github.com/mafintosh/peerflix


Mounting torrent-streams to the file system? YES: torrent-mount

just call # torrent-mount <magnet link>

The ultimate? Can you install Ubuntu in real time? with streaming?

YES - torrent-mount a ubuntu install magnet link
then reading the file with virtualbox and installing ubuntu in a new image <- WORKS, but a bit slow

## STOP BEING PERFECT - @angustweets

British, live in America, work for Twitter, frontend infrastructure team

Writing a book: "IF HEMINGWAY WROTE JAVASCRIPT"


### JavaScript

10 % deceptively familiar syntax
90 % weird shit

typeof NAN = "number"


### Why do we need imperfection?

#### 1. technology thrives on Open Minds
"Behold, this comma operator"


#### 2. Context > dogma
"Wow such call-backs!"
examples: classical inheritance is for many considered good standard.
Javascript prototypical inheritance is actually classical inheritance

inheritance in javascript takes alot of code and this is why people hate javascript.

Solution: throw out OO entirely

Google style guides says to use primitives vs constructors,
But the google v8 performance tuning talk tells you to use new Array(num) for better performacne in hot code.

Douglas crookford says to always use triple equals (===)
But how about 'typeof x == "function"'? That's fine because typeof always returns a string.

#### 3. Play == Learning

Remember to distinguish between play and professional work

JavaScript is not a Science
Your code will break - it always does.
Keep it simple and human readable so its easier to fix.

Dont taake anything i've said too seriou. I'm just exploring.

# Day 2

## Seeing Types in JavaScript - Marijn Haverbeke - @marijnjh
ternjs.net  attempt of improving javascript editor integration.

- has autocomplete
- types of parameters of APIs
- jump to definition
- refactor names
- infer types such that .t suggests .toString() for strings

Done by parsing the code to an AST (abstract syntax tree)

Parsing of syntactically invalid code is possible by cleaning up the code in the background.

Types are inferred by observation of assignment

Type inference is not easy - e.g. look at coffeescript inheritance - copying/changing prototypes 

### real world coding
Pretty fast: 10 000 lines/sec - not fast enough. you don't want to wait 3 seconds for your autocomplete 
solution: Only parse file where changes are made, keep data from previous analysis runs on other files.

Parsing of requireJS/commonJS - keep a "budget" for each dependency and simply stop analyzing when the amount of parsed expressions have reached a threshold.

Plugins for Emacs, Vim, & Sublime Text
- install editor plugin
- add .tern-project file
- go

Not perfect, it's fuzzy analysis, doesnt always work. In static language you can rely on autocomplete, but this is javascript (dynamic) but it still has value with some limited autocompletion.

Alternatives: simply run the program - cut off side effects - and simply keep the types from the run.

The ultimate solution would probably be the best of both worlds: runtime inference and statical analysis/parsing.

github.com/marijnh/tern

## Not Mobile-Unfriendly UI Components With React - Arne Martin Aurlien - @arnemart

Befungius - enterprise level befunge interpreter - super fast tracing JIT compiler - voxel.js based editor
j/k (sorry)

### React
Yet another javascript UI lirbary - has some special tricks
Created by Facebook
About creating self.contained reusable UI components - no routing - not full stack framework
Some use it as V as in MVC  some use it with backbone - but you dont need to do classic MVC at all

React was created because the DOM is stupid - hard to work with - statefull mess.
Frameworks proveid two-way binding betwen UI and app state - angulare/ember/backbone/knockout - can get really messy if your not deciplined. You often get tight coupling between controllers and models.

React tries to solve this - by having very loose coupling between components.
React allows you to do one way databinding - the "flux" pattern

React will rerender your entire applicatione every time there is an update. Treat your app like a stateless web app. But isn't the DOM too slow to do this? YES its terribly slow.
Solution: implement virtual DOM - rerender into the virtualDOM, which is then diffed to the real DOM, which then calculates the minimum amount of changes.

React has stupid naming: React.createClass <- author was high as a kite

-- live coding --

#### Side note 1: jsx - theres always a catch
JS: Not good enough
JSX: crazy way of inserting html into the DOM 

#### Mobile?
What do i do to make my component mobile-friendly? General rules applies

Not a whole lot:

- dont be an idiot (dont rely on hovering,.. etc)

If you need touchEvents:

    React.initializeTouchEvents(true); // will go away in the future?

#### Side note 2: Topcoat
CSS library by Adobe - "fast clean web apps" - react library react-topcoat

-- live coding --

React components have both "props" and "state"

props are things which are sent into a component - will always be passed in and a component should never try to change them
state is internal state to a specific cokmponent - should never be changed by outside components. Usually changed by component that owns it by result of user interaction

-- live coding --

componentDidUpdate <- called whenever the component is updated. Can be used to save the state of the component into local storage 
Use getInitialState to retrieve data from local storage

#### Side note 3: error messages

Error messages are really good when developing with react and node

### Summary

React exists.
I've enjoyed using it. You should try it. Solid library.

Slides/everything is availanle at github.

Not a fan of full stack frameworks. 

## Geography for Web Mapping: the Good, the Bad, and the Stuff You Can Forget - Camille Teicheira @fulgenteft

slides on github and twitter

### "intro to neogeography"

maptime.io

Why are people interested in maps? Because representation is important.

Alot of customizations are possible with open street maps

custom directions: routes for scooters -> avoid high speed roads, hills etc..

#### Geodata

(lng, lat) === (x,y) <- geoJSON

node: topoJSON
.. but jut use geojson unless you have problems with size of files

#### What do i do with this data?

1. commit geoJSOn to github
2. mapbox.com create a account and upload files 
3. use a mapping library leaflet.js  (tilemill, tilemill, etc)

tilemill = use css to change color of parts of the maps

## Got TLS? An overview of why you need it and how to do it right. - Parisa Tabriz @laparisa

slides: bit.ly/gottls

### What's TLS? formerly known as SSL

Transport layer security
Provide security communication over the internet

TLS heart of https
privacy via encryption
data integrity <- no snooping tampering

TLS prevents "man in the middle attacks"

Assume no data security if your not using TLS

### firesheep
Exploited downgrade vector on open wifi

looked at cookie headers, hijacks those and lets other snoop on others sessions on facebook etc.

### A site without TLS is saying "i dont care about the privacy and security of my users"

### How to get TLS and debunk some myths

Excuses: "dont have TLS becaus eof performance/cost" Legitimate concern 10 years ago. Not today.

TLS performance tune-ip:  istlsfastyet.com

Free SSL certificates startssl.com <- personal use

TLS is easy to deploy - easy to make some mistakes too

### Get TLS right

expired certificates 30 % traffic drop <- 70 % of users dont care!

1. support only HTTP
2. support only HTTPS <- best state of security
3. support both <- here is where downgrade situations happen <- not good

Browsers will block any kind of active mixed content  eg https page including http css/js/other resources

Solution:
1. use relative URLS
2. omitting the scheme completely


http header attributes:

    Secure: HttpOnly

    Strict-Transport-Security: max-age=60000;
    includeSubDomains

TLS is not a security silver bullet:

1. some information leaks possible
2. no protection against IP-level threats
3. Other web security bugs may remain.

TLS piggybacks on HTTP

TLS does not protect against DDoS, etc..

## The ghost of javascript future - James "substack" halliday - @substack

Some of the layers in the software stack will probably stick for very long. posix/unix.. 

The earth will basically melt in 600 million years
So how are we gonna survive? 

There are some things we need:

1. necessary:
npm
nodejsbrowsers
browserify
etc

We should probably spend more time documenting what we do 
e.g. browserify-handbook @ github

2. Have fun:
studio.substack.net/-/recent
Having fun is so important, we should embrace it more in programming
Make things more approachable and interesting

p2p maps:

peermaps - use torrent-stream to stream maps from well seeded open source map torrents

Make things that just need to exist, such that we can take them for granted, such that we can hack the planet


Work on things immediately when you have an idea.. You are motivated when you have an idea, and it will probably go awawy if you sit on it too long.

How do you get time? Live cheaply.... i guess?
The most important thing is that they are fun!


