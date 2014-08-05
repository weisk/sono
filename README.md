# Sono

A small library for managing sound in the browser.


### Current WIP API

var Sono = require('Sono');


#### main api

Sono.context // the WebAudio context

[static] Sono.VERSION // current version

##### add / get sounds:

Sono.add(key, data, loop)

Sono.get(key) // returns a WebAudioPlayer or HTMLSound

* var sound = Sono.get('someKey');
* sound.play()
* Sono.get('someKey').play()

##### controls:

Sono.mute() // master

Sono.unMute() // master

Sono.pauseAll() // all currently playing

Sono.resumeAll() // all currently paused

Sono.stopAll() // all

Sono.play(key) // individual sound

Sono.pause(key) // individual sound

Sono.stop(key) // individual sound

##### loading:

[internal] Sono.initLoader()

Sono.load(key, url, loop, callback, callbackContext, asBuffer)

* Sono.load('someKey', 'audio/foo.ogg', false, onSoundLoaded, this, true); // loads this file
* Sono.load('someKey', ['audio/foo.ogg', 'audio/foo.mp3']); // loads first one that works
* Sono.load('someKey', ['audio/foo.ogg', 'audio/foo.mp3']).play(); // plays sound when loaded

Sono.loadBuffer(key, url, loop, callback, callbackContext) // load as array buffer

Sono.loadAudioTag(key, url, loop, callback, callbackContext) // load as html audio el

Sono.destroy(key) // remove, stop and cancel if still loading (should it be called remove?)

##### set up / detection:

[internal]?? Sono.createAudioContext()

[internal]?? Sono.getSupportedFile(fileNames) // accepts single string, array or object and attempts to return best supported file

* Sono.getSupportedFile(['audio/foo.ogg', 'audio/foo.mp3'])
* Sono.getSupportedFile({ foo: 'audio/foo.ogg', bar: 'audio/foo.mp3'})
* Sono.getSupportedFile('audio/foo') // adds first detected extension (.ogg, .mp3, etc)
* Sono.getSupportedFile('audio/foo.ogg')

[internal]?? Sono.getExtension(fileName)

[internal]?? Sono.getSupportedExtensions()

##### handle mobile device touch lock:

[internal]?? Sono.handleTouchlock()

##### pause/resume on page visibility change:

[internal]?? Sono.handlePageVisibility()

##### logs info about Sono version and current browser:

Sono.log()

##### get support info:

get Sono.isSupported // is audio supported at all?

get Sono.hasWebAudio // is WebAudio supported?

##### volume:

get/set Sono.volume

##### getter to access node factory:

get Sono.create

##### getter to access loader:

get Sono.loader

##### getter to access utils:

get Sono.utils


#### Sono.create (node factory module)

Sono.create.gain(value)

Sono.create.pan()

Sono.create.filter.lowpass(frequency)

Sono.create.filter.highpass(frequency)

Sono.create.filter.bandpass(frequency)

Sono.create.filter.lowshelf(frequency)

Sono.create.filter.highshelf(frequency)

Sono.create.filter.peaking(frequency)

Sono.create.filter.notch(frequency)

Sono.create.filter.allpass(frequency)

Sono.create.delay(input, time, gain)

Sono.create.convolver(impulseResponse)

Sono.create.reverb(seconds, decay, reverse)

Sono.create.createImpulseResponse(seconds, decay, reverse)

Sono.create.analyser(fftSize)

Sono.create.compressor()

Sono.create.distortion()

Sono.create.scriptProcessor(bufferSize, inputChannels, outputChannels, callback, callbackContext)

#### Sono.utils (helper utils module)

Sono.utils.fade(gainNode, value, duration)

NOTE: should pan stuff be moed into pan module? (i.e. Sono.utils.pan() returns pan module?)

Sono.utils.panX(panner, value)

Sono.utils.pan(panner, x, y, z)

Sono.utils.setSourcePosition(panner, positionVec)

Sono.utils.setSourceOrientation(panner, forwardVec) // forwardVec = THREE.Vector3

Sono.utils.setListenerPosition(positionVec)

Sono.utils.setListenerOrientation(forwardVec) // forwardVec = THREE.Vector3

Sono.utils.doppler(panner, x, y, z, deltaX, deltaY, deltaZ, deltaTime)

Sono.utils.filter(filterNode, value, quality, gain)

Sono.utils.getFrequency(value) // return a freq value by passing 0-1

Sono.utils.createMicrophoneSource(stream, connectTo) // should prob go into .create

Sono.utils.distort(value)

#### Sono.loader (loader module)

Sono.loader



## Notes

Inconsistencies:

* HTMLSound has get/set volume and WebAudioSound doesn't
* WebAudioSound has get source and HTMLSound doesn't




