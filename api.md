---
layout: default
title: API
---

<p style="color:#F00">
API: A listing of all the JavaScript functions and PureData objects made available by the DBM.
</p>

## API

The following JavaScript functions and PureData objects provide a way to communicate your HTML GUIs with your PD patches. The API is heavily based on the [libpd low-level C API](https://github.com/libpd/libpd/wiki/libpd).

All the javascript functions are callback based and will trigger success or error callbacks upon completion.

### Initializing and managing patches

Depending on the run environment, this functions and objects will initalize communication between the web browser and Pure Data (debug mode), or they will start the audio engine and open PD patches.

#### JavaScript

* **initialize: function(success, error)**  This function is called implicitly by other functions, no need to call it yourself.
* **clearSearchPath: function(success, error)**  Clears the search path of PD.
* **addToSearchPath: function(path, success, error)**  Adds a directory to the search path of PD.
* **openFile: function(dir, file, success, error)**  Reads a patch with the given file name from the given directory. The success callback has one parameter which is an identifier for the open file.
* **closeFile: function(file, success, error)**  Closes the file given by the file identifier (as returned by openFile).
* **dollarZeroForFile: function(file, success, error)**  Returns the $0 tag for the given file.
* **configureTicksPerBuffer: function(ticksPerBuffer, success, error)**  PureData processes sound in frames of 64 samples. With this function, you can configure how many 64 sample frames PD processes in each audio callback. You probably don't need to set this to anything different than the defaults.
* **setActive: function(active)**  Enables DSP processing in the PD patch.
* **getActive: function(success, error)**  The active parameter in the callback success callback function will indicate if DSP processing is enabled in PD.
* **configurePlayback: function(sampleRate, numberChannels, inputEnabled, mixingEnabled, success, error)**  Initializes the audio engine with the specified parameters. The audio engine may change the initialization parameters so you should check for them in the success callback:

```js
PureData.configurePlayback(44100, 2, false, false, 
function(params){
  // Success, do something with params.sampleRate, 
  // params.numChannels, params.inputEnabled, params.mixingEnabled
});
```

#### PureData

* **[dbm-connect]**  Instantiate this object in your main PD patch to establish communication with the JavaScript API. Internally, it will route messages to the correct receivers and manage the communication according to the run environment.
* **[websocket-server]** This is a lower-level object that you won't have to instantiate yourself. It is used by [dbm-connect] to talk to a web browser using websockets. You are free to use this outside Dancing Bone Machine to communicate PD with webbrowsers/servers. Internally, it is based on libwebsockets.

### Sending messages to PD

* **sendBang: function(receiver)**  Send a bang to the receiver. `PD.sendBang('foo')` acts just like sending a bang to [send foo] in PD.
* **sendFloat: function(value, receiver)**  
* **sendSymbol: function(value, receiver)**  
* **sendList: function(list, receiver)**  
* **sendMessage: function(list, receiver, symbol)** Send a typed message to the given receive symbol. Ex, `PD.sendMessage([1], 'dsp', 'pd')` is the same as clicking `[pd; dsp 1(` in PD.

### Receiving messages from PD

These functions allow you to register/unregister callbacks that work like the PD [receive] object. In this example, the callback function will run whenever something is sent to a [send foobar] object in PD.

```js
PureData.bind('foobar', function(value){
    console.log(value);
});
```

* **bind: function(sender, callback)**  
* **unbind: function(sender)**  
* **unbindAll: function()**  

### Accessing arrays

* **arraySize: function(arrayName, success, error)**  The success callback will give a parameter with the size of a named [array] or [table] object in PD.
* **readArray: function(arrayName, n, offset, success, error)**  The success callback will give an array with float values contained in a named [array] or [table] object in PD.
* **writeArray: function(arrayName, data, success, error)**  This function writes float data points to a named [array] or [table] object in PD.

### Sending MIDI events to PD

#### Javascript

These functions work in a similar way to the sendBanf, sendFloat, etc functions above.

* **sendNoteOn: function(channel, pitch, velocity)**  
* **sendControlChange: function(channel, controller, value)**  
* **sendProgramChange: function(channel, program)**  
* **sendPitchBend: function(channel, value)**  
* **sendAfterTouch: function(channel, value)**  
* **sendPolyAfterTouch: function(channel, pitch, value)**  
* **sendMidiByte: function(port, value)**  
* **sendSysEx: function(port, value)**  
* **sendSysRealTime: function(port, value)**  

#### PD

To receive MIDI events in your patch you should use the following blocks instead of the usual [notein], [ctlin], etc. objects.

* **[dbm-notein]**
* **[dbm-bendin]**
* **[dbm-ctlin]**
* **[dbm-polytouchin]**
* **[dbm-midiin]**
* **[dbm-sysexin]**
* **[dbm-touchin]**
* **[dbm-pgmin]**
* **[dbm-midirealtimein]**

### Receiving MIDI events from PD

Similar to the recieve message functions above, thie callbacks are triggered when MIDI events are sent from the PD patch.

#### JavaScript

* **bindMidiNoteOn: function(callback)**  
* **bindMidiControlChange: function(callback)**  
* **bindMidiProgramChange: function(callback)**  
* **bindMidiPitchBend: function(callback)**  
* **bindMidiAfterTouch: function(callback)**  
* **bindMidiPolyAfterTouch: function(callback)**  
* **bindMidiByte: function(callback)**  
* **bindPrint: function(callback)**  

#### PD

Similar to the midi receive objects, you must use the following MIDI send objects in PD so the respective JavaScript callbacks are triggered.

* **[dbm-bendout]**
* **[dbm-ctlout]**
* **[dbm-midiout]**
* **[dbm-noteout]**
* **[dbm-pgmout]**
* **[dbm-polytouchout]**
* **[dbm-touchout]**

