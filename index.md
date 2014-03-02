---
layout: default
title: Create music applications with PureData and HTML.
---

<p style="color:#F00">
This website will be restructured into new sections as explained below. Some sections are now complete so go ahead and click.
</p>

<p style="color:#F00">
Overview: Very short. What the DBM is about in a nutshell. This section needs to be updated according to the new (easier) way of including DBM into new projects.
</p>

<p style="color:#F00">
Prerequisites: Stuff outside of the scope of this documentations that users should know in order to build a successful musical app. Completed.
</p>

<p style="color:#F00">
Guide: The "user's manual". A step by step guide that shows users around everything in the toolkit. 
</p>

<p style="color:#F00">
Tutorial/Example: Shows how the example application was created in the form of a step by step tutorial.
</p>

<p style="color:#F00">
API: A listing of all the JavaScript functions and PureData objects made available by the DBM.
</p>

## Overview

The Dancing Bone Machine is a toolkit that allows you to create audio and music applications and plug-ins for different platforms and hosts using [PureData](http://puredata.info) and HTML.

**In a nutshell:**

``` bash
$ git clone https://github.com/dancing-bone-machine/dancing-bone-machine.git
$ cd dancing-bone-machine
$ git submodule update --init --recursive
# ...create your awesome PD patches and HTML pages...
$ scripts/generate-ios-wrapper.sh  
$ profit
```

### Development and debugging workflow that makes sense.
 
You'll be able to run and debug the HTML portions of your app in your favorite [webkit based web browser](http://en.wikipedia.org/wiki/WebKit#Use) while editing and running your PD patch in either [Pure Data](http://puredata.info/downloads/pure-data) or [Pd-extended](http://puredata.info/downloads/pd-extended). Using our simple JavaScript API and a set of PD objects you can establish communication between them without having to run your app in an emulator or any other weird environment.

This is possible thanks to our [[websockets_server]](https://github.com/dancing-bone-machine/dancing-bone-machine/tree/master/library/dancing-bone-machine/pd/externals/src/websocket_server) object in PD.

If you don't plan on distributing your application, this setup might be all you need.

### Wrap and export

A set of generator scripts are also included. These allow for creating native applications for several platforms where you can run your application. Currently only iOS is supported, but more platforms are planned: [VST](http://en.wikipedia.org/wiki/Virtual_Studio_Technology) plug-ins, Android, [LV2](http://lv2plug.in/) plug-ins, and [JACK](http://jackaudio.org/) apps for Linux.

### What!?

If none of this makes sense to you, but you still want to make some musical software, head to the [prerequisites section](/prerequisites.html) and spend some time reading the linked resources, you'll be fine when you come back ;)


### Licensing

The Dancing Bone Machine toolkit is licensed under the [GNU Lesser General Public License with a static linking exception](https://github.com/dancing-bone-machine/dancing-bone-machine/blob/master/COPYING). All of the examples are licensed under the [GNU General Public License](http://www.gnu.org/licenses/gpl.html).

In other words:

* You get the full source code for Dancing Bone Machine. You can examine the code, modify it and share your modified code under the terms of the LGPL.
* Dancing Bone Machine is safe for use in closed-source applications. The LGPL share-alike terms do not apply to applications built with Dancing Bone Machine. The LGPL applies to Dancing Bone Machine own source code, not your applications.

### Acknowledgements

Dancing Bone Machine uses code from a number of projects, their respective licenses are in the source code.

* [libpd](http://libpd.cc/)
* [Apache Cordova](http://cordova.apache.org/)
* [RequireJS](http://requirejs.org)
* [libwebsockets](http://libwebsockets.org)
* [stringencoders](http://code.google.com/p/stringencoders)

