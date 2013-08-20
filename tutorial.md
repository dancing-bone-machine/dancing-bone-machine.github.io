---
layout: default
title: Tutorial
---

## Tutorial

This tutorial explains how to build a simple synthesizer using the Dancing Bone Machine toolkit. You should be familiarized with using a command line terminal, HTML and JavaScript programming and PureData. If you're not, I suggest you go learn a little bit about them and then come back here. For PureData, I recommend you read the manual at [flossmanuales.net](http://flossmanuals.net/puredata/).

You can view or download the full source code for this tutorial [here](https://github.com/dancing-bone-machine/example)

Here's what we are going to build:

<div style="text-align:center">
    <iframe src="http://player.vimeo.com/video/72626468" width="250" frameborder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe> 

    <iframe src="http://player.vimeo.com/video/72626818" width="250" frameborder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>
</div>

### 1. Download the Dancing Bone Machine toolkit

Fire up a terminal and clone the git repository. If you haven't heard about git, I suggest you take a look at [this](http://www.codeschool.com/courses/try-git).

```bash
$ git clone https://github.com/dancing-bone-machine/dancing-bone-machine example-app
$ cd example-app
$ git submodule update --init --recursive
```

### 2. Build a simple synth in PD

I assume you know your way around PD so I'm not going to go into a lot of detail here. Take a look at the patch we'll use:

<a href="images/synth.png"><img src="images/synth.png" width="100%"></a>

The patch must be saved in the app/pd/patches directory.

The [oscillator] object is a simple sound generator that lets you set it's waveform by crossfading between a sine wave, a square wave and a sawtooth wave. Notice we're setting it's waveform value with the [receive waveform] block. To set it's frequency, we use a midi notein value and the [mtof] object. 

The midi velocity value is used to calculate a simple line envelope and the [receive volume] signal is used to set the amplitude value of the oscillator.

We are also storing 512 samples of the output signals every 100 millliseconds into the [table graph1 512] object. This will be used to plto the wave in the HTML interface.

#### The important things to notice in the patch

[dbs-connect] is used to establish communication between your patch and the HTML part of your app.

Instead of using the regular [notein] object, we're using [dbs-notein]. They behave equally but [dbs-notein] receives midi events from both actual midi ports and from the HTML interface.

### 3. Build a graphical user interface using HTML

Your HTML application must live in the app/html/index.html file. You can also have stlesheets, scripts and other assets in there. Again, I will only highlight the important parts, you can look at the details in the [HTML](https://github.com/dancing-bone-machine/example/blob/master/app/html/index.html) and [JavaScript](https://github.com/dancing-bone-machine/example/blob/master/app/html/scripts/sample-app.js) files.

Note that the `scripts/dancing-bone-machine/dancing-bone-machine.js` script must be loaded by the HTML.

Here is what the interface looks like when rendered in a browser.

<p style="max-width:452px; margin: 0px auto"> <a href="images/gui.png" ><img src="images/gui.png" width="100%"></a> </p>

#### Knobs

The knobs were created using [jQuery Knob](http://anthonyterrien.com/knob/):

```html
<input id="volume" type="tel" class="knob" value="50" data-min="0" data-max="100" />
```

```js
var w = $('#controls').innerWidth();
var h = $('#controls').innerHeight();
var options = {
    'fgColor': '#ffec03',
    'inputColor': '#ffec03',
    'bgColor': '#444444',
    'angleOffset': '-125',
    'angleArc': '250',
    'width': Math.ceil(w * 0.25),
    'height': Math.ceil(w * '0.22')
};

var opts2;
// Volume
opts2 = $.extend({'change': function(v){
    PD.sendFloat(v/100, 'volume');
}}, options);
$("#volume").knob( opts2 );
```

#### Piano Keyboard

The piano keyboard was created using a simple background [image](https://github.com/dancing-bone-machine/example/blob/master/app/html/styles/piano.png) and some divs to capture mouse/touch events.

```html
<div id="piano-scroll">
 <div id="piano">
    <div class="octave" data-octave="4">
       <div class="key white" data-note-number="0"></div>
       <div class="key white" data-note-number="2"></div>
       <div class="key white" data-note-number="4"></div>
       <div class="key white" data-note-number="5"></div>
       <div class="key white" data-note-number="7"></div>
       <div class="key white" data-note-number="9"></div>
       <div class="key white" data-note-number="11"></div>
       <div class="blacks">
          <div class="key" data-note-number="1"></div>
          <div class="key more-margin" data-note-number="3"></div>
          <div class="key" data-note-number="6"></div>
          <div class="key" data-note-number="8"></div>
          <div class="key" data-note-number="10"></div>
       </div>
    </div>
```

```js
this.pressedKey = function(event){
  event.preventDefault();
  
  // Calculate midi note number and send midi note on event
  var key = $(event.currentTarget);
  var octaveNumber = key.closest('.octave').attr('data-octave');
  var noteNumber = octaveNumber*12 + Number(key.attr('data-note-number'));
  $(key).addClass("pressed");
  lastKey=key;
  playingNote=noteNumber;
  PD.sendNoteOn(0, noteNumber, 65);
};

this.releasedKey = function(event){
  event.preventDefault();

  $(lastKey).removeClass("pressed");
  PD.sendNoteOn(0, playingNote, 0);
  playingNote = -1;
};
```

#### Oscilloscope

The oscilloscope was created using the &lt;canvas&gt; tag and JavaScript API.

```js
oscilloscope.context.strokeStyle="#FFEC03";
var y = 0;
var i = 0;
var j = 0;
for(i=0; i<oscilloscope.w; i=i+oscilloscope.jumpPixels){
   y = oscilloscope.scale + oscilloscope.scale*points[j*oscilloscope.jumpPoints];
   oscilloscope.context.lineTo(i,y);
   oscilloscope.context.stroke();
   j++;
}
```

#### Opening the patch and sending messages

Here's the core of all this. To establish communication with the PD patch and send messages, you need to use the Dancing Bone Machine JavaScript API like so:

```js
PD.configurePlayback(44100, 2, false, false, function(){
   PD.openFile('pd/patches', 'synth.pd', function(){
      PD.setActive(true);
      PD.sendFloat(0.5, 'waveform');
      PD.sendFloat(0.5, 'volume');
   });
});

//...

PD.sendNoteOn(0, noteNumber, 65);
```

### 4. Running in debug mode

The simplest way to run your app is to open the index.html file in a browser and the synth.pd patch in either Pure Data or Pd-extended. You must add the library/dancing-bone-machine/pd/externals/bin directory to the PureData search path so that the externals and abstractions that we provide can be found by PD.

### 5. Generating an iOS wrapper application

A generator script is included as part of Dancing Bone Machine. You can use it as follows:

```bash
$ cd path/to/project
$ scripts/create-ios-wrapper.sh
```

This will create an Xcode project with all the configurations needed to run your HTML interface and your PD patch within an iOS application. Open the `app/wrappers/ios/DancingBoneMachine.xcodeproj` project with Xcode and follow [Apple's guidelines](https://developer.apple.com/devcenter/ios/index.action) to run the app in the iOS simulator or in an actual iOS device.
