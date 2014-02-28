---
layout: default
title: Prerequisites
---

## You should know this stuff first

### tl;dr

<span style="font-size:17px;">There is a lot of material here. If you want to skip everything else, take a look at [this](http://www.pd-tutorial.com).</span>

<hr/>

Although The Dancing Bone Machine toolkit hides a lot of the complexities associated with building musical software, like [real time](http://www.cs.cmu.edu/~rbd/doc/icmc2005workshop/real-time-systems-concepts-design-patterns.p) [constraints](http://www.rossbencina.com/code/real-time-audio-programming-101-time-waits-for-nothing) and cross-platform particularities, there are some basic musical, aesthetic and technical skills and outlooks you should have in order to successfully design and build musical software. This page is a very brief and incomplete directory of these things with suggestions on where to go and learn about them.
    
If you know what things like square waves, fourier analysis, sequencers, MIDI, pitch, temperament or chords mean, you can probably skip this section and go to the [guide](guide.html) where you'll learn how to put things together with The Dancing Bone Machine toolkit and start making some sounds. I suggest, however, that you **at least skim through this page**.

Also, when building your apps, you will spend most of your time with [PureData](#puredata) and [HTML](#html) so get ready to become an HTML and PD ninja in the process.


### Know what you like

This one might sound obvious, but you really need to know what sounds good and bad to you, if someone asks you what kind of music you like or what your favorite musician is and you don't care too much for the answer, you probably need to go out and listen to more music. A lot more. Pay attention to what makes it appealing for you, find out who composed and who plays it, look for similar artists to the ones you like. This is such a broad and never-ending topic that I won't even attempt to give you any links to get started, go and ask your friends to show you that cool record they were playing the other day.

Very importantly, find out which musical instruments, software and other tools are your favorite musicians using. Perhaps most of them are using the same kinds of instruments or software? Is the sonority of their choice of instruments or tools influencing the fact that you like them? If so, you should find out how those instruments work, are they easy or hard to play? Perhaps if you added a little thing or two, would they sound better or be easier to play? Can you imagine how you would implement such instruments in software and change their designs or sound?

### Learn a little bit about how music and sound works

You are going to be writing software that makes or transform sound and music so it will be really useful to know how they work and how they relate to each other. 

You can, of course, start making sounds and looking for things that work by trial and error but humanity has a tremendous head start of several centuries and there are a lot of tricks and techniques already out there that can help your creations sound good. It's called music theory. You could spend several years learning it and become a master composer or instrumentalist but for our purposes, you just need to learn a little bit of it. 

A fun but perhaps lengthy way of learning about it is to pick up a musical instrument and find yourself a good teacher or book. As you go along, you will learn things like the name of the musical notes, how to choose them from musical scales, how to put together several notes into chords that sound harmoniously and many more useful tricks that will be useful when creating musical software. Here is a [nice little writeup](http://www.wikihow.com/Learn-to-Play-an-Instrument) on how to learn to play a "traditional" musical instrument. 

If trombones, drums, guitars or keyboards are not your thing, or if you are in a hurry, there is a newer kind of musical instrument that will allow you to start playing with notes and learn some concepts of music theory right away: the digital audio workstation (more about them below). You can go ahead and choose one that appeals to you, and look for resources like "basic music theory for electronic musicians", you'll probably be up and running in a few days. [Here](http://music.stackexchange.com/questions/12180/want-to-learn-composing-and-producing-music-on-daws-where-to-start-from) is a nice discussion about this and the following are some resources that were useful to me (look for other info, too!):

* [Music theory articles at the Ableton Cookbook blog](http://www.anthonyarroyodotcom.com/theabletoncookbook/tag/music-theory/).
* [Videos on Youtube](https://www.youtube.com/user/DaveCoutureMusic) [about music theory](https://www.youtube.com/watch?v=syJf4Ysmeuc&list=RDS2JN_0LPQK0)
(you'll find plenty more).
* [The Music Theory for Computer Musicians book](http://www.amazon.com/Theory-Computer-Musicians-Michael-Hewitt/dp/1598635034).

Now, it's also important and useful to understand how sound and music work at the physical level. Why does a guitar string sound when you strike it? What's the deal with vibrations? How does musical pitch relate to frequency? [The physics classroom](http://www.physicsclassroom.com/class/sound) has a nice tutorial about this topics, go check it out. There is also a more lengthy explanation from David Lapp in [his book](http://kellerphysics.com/acoustics/Lappp), have a read if you want to know a bit more.

### Know what's already out there

Re-implementing something that has already been made can be useful and a nice learning experience but you probably don't want to spend countless nights of implementing your next killer musical instrument and then find out it has already been made and that it's available for cheap, for free or open-sourced. You will also get valuable ideas and questions by studying what other instruments and tools have already been made and what kinds of music is being produced with it. 

So, go and find out what kinds of electronic instruments are out there (you won't be designing acoustic instruments with The Dancing Bone Machine), who's making them, who's using them and how. Below is a list of links that will get you started.  Also, don't forget to go to your local musical instrument shop and see what they have. Ask them to connect an instrument or three for you to play with and if they have a money-back policy, take something home with you for a few days ;) Magazines about electronic music making are also a good resource.

* Here are [two](http://wiki.linuxaudio.org/apps/start) [lists](http://www.synthzone.com/digaudio.htm) of audio and music software. The ones I use the most are [Ableton](https://www.ableton.com/) and [Ardour](http://ardour.org/).
* And [three](http://audiob.us/apps/) [more](http://www.iosmusician.com/app-lists) [lists](http://idesignsound.com/) focused on music and audio applications for mobile devices.
* The [Create Digital Music](http://createdigitalmusic.com/) and [Create Digital Noise](http://createdigitalnoise.com/) blogs write about some really cutting-edge stuff. Don't miss them.
* [120 Years of Electronic Music](http://120years.net/wordpress/) is a lengthy history of electronic musical instruments.
* Here are a [couple](http://www.musicradar.com/computermusic) of [magazines](http://digitalmusicianonline.com/author/mnorth/).
* And [some](http://en.wikipedia.org/wiki/Electronic_musical_instrument) [wikipedia](http://en.wikipedia.org/wiki/List_of_musical_instruments#Electronic_instruments_.28electrophones.29) [articles](http://en.wikipedia.org/wiki/Synthesizer).

### Leave plenty of room for weirdness

Having said all of the above, not everything should be harmonic or in-key and all the only possible instrument types have not been invented. You would not be the first to do such strange things, either, there has been some pretty weird movements like [atonality](http://en.wikipedia.org/wiki/Twelve-tone_technique) and [electro acoustic](http://en.wikipedia.org/wiki/Electroacoustic_music) music in the 20th century and some really strange contemporary stuff like [black midi](http://gawker.com/black-midi-is-insane-but-totally-mesmerizing-robot-mu-1373444675). So please, do go crazy! :D

### <a id="puredata"></a>Find out how to make the sounds you want using code

All right, so we finally arrived to the fun part: how to make all those cool sounds with computer code? There are many ways, but the one we integrated into the Dancing Bone Machine is by making PureData programs (they are called patches). The following are some really nice resources for learning how to make sounds and music with PD.

* This is my favorite one and the one you can't miss. The [Programming Electronic Music With PureData](http://www.pd-tutorial.com/) by Johannes Kreidler.
* The PureData manual at flossmanuals.net has a really neat section on making audio with PD.
* The [Designing Sound](https://mitpress.mit.edu/books/designing-sound) book is a great and lengthy resource on sound design, with all examples in PD.

If you want do go deeper and understand how PureData and other computer music systems do what they do, the following resources are a good start.

* [The Theory and Techique of Electronic Music](https://mitpress.mit.edu/books/designing-sound) by Miller Puckette, PD's inventor.
* [The Computer Music Tutorial](http://www.amazon.com/Computer-Music-Tutorial-Curtis-Roads/dp/0262680823) by Curtis Roads.
* [The Audio Programming Book](http://mitpress.mit.edu/books/audio-programming-book) is the bible of low-level programming for audio. One of my favorite resources.

### <a id="html"></a>Build interactivity and looks

The other part of DBM applications that you have to take care of is the graphical user interface (GUI). We chose the HTML language (which is actually a combination of HTML, JavaScript and Cascading Style Sheets) for building GUIs because of it's huge popularity and it's capability to run on almost every computing platform out there. So, if you don't know at least some basic HTML and Javascript, go and find yourself some nice [tutorials](https://duckduckgo.com/?q=html+and+javascript+for+beginners+tutorials&kl=us-en) and take a look at the following resources:


HTML, GUIs


### Have fun and be nice

This is supposed to be fun, if you're bored, your sounds/apps will  sound boring
ask nicely, this is open source.
