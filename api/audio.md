# Audio

## Class: AudioManager

~~~
import AudioManager;
~~~

For the examples on this page, we'll assume the following
directory structure of a project:

~~~
project
.
├── manifest.json
├── sdk/ -> /path/to/basil/sdk
├── build/
├── resources/
│   └── sounds/
│       ├── music/
│       │   └── levelmusic.mp3
│       └── effect/
│           └── boink.mp3
└── src/
    └── Application.js
~~~

### new AudioManager ([options])
1. `options {object}`
	* `path {string}` ---Directory path containing audio files.
	* `files {object}` ---Collection of audio files mapped to their options.
	* `persist {}`

`path` is the directory containing a group of audio files,
relative to the top-level of a project. `files` is an object
mapping audio files to their options.

The `files` options object has the following properties:

 * `sources {}`
 * `background {boolean}` ---Set as the background music file, one per group.
 * `loop {boolean}`
 * `volume {number}`
 * `path {string}` ---Add addtional path information to the options path.

Given the above directory structure for a project, multiple
sound groups can be created using:

~~~
var audiomanager = new AudioManager({
  path: 'resources/audiomanagers',
  files: {
    levelmusic: {
      path: 'music',
      volume: 0.5,
      background: true,
      loop: true
    },
    boink: {
      path: 'effect',
      background: false
    }
  }
});
~~~

### audiomanager.addSound (name [, options])
1. `name {string}`
2. `options {object}` ---Audio file options described above.

Add a sound to the sound group.

~~~
audiomanager.addSound ('pop', {
  path: 'effect',
  background: false
});
~~~

### audiomanager.play (name [, options])
1. `name {string}`
2. `options {object}`
	* `loop {boolean} = false`
3. Return: `{boolean}` ---Returns `true` on success, `false` if not.

Play a audiomanager. If it has already been preloaded, it will play
immediately, otherwise, it will need to load it into memory
before playing.

~~~
audiomanager.play('boink', {loop: true});
~~~

### audiomanager.pause (name)
1. `name {string}`
2. Return: `{boolean}` ---Returns `true` on success, `false` if not.

Pause a sound. The audio file is stopped at a certain point,
and restarted from that point when played again.

~~~
audiomanager.play('levelmusic');
~~~

### audiomanager.stop (name)
1. `name {string}`
2. Return: `{boolean}` ---Returns `true` on success, `false` if not.

Stop a sound. If a sound is played again, it will restart
from the beginning.

~~~
audiomanager.stop('levelmusic');
~~~

### audiomanager.setVolume (name, volume)
1. `name {string}`
2. `volume {number}` ---A range between 0 and 1.
3. Return: `{boolean}` ---Returns `true` on success, `false` if not.

Sets the volume of the sound, with 1 as the maximum, and 0
as silent. A sound's default volume is 1.

~~~
audiomanager.setVolume('levelmusic', 0.8);
~~~

### audiomanager.getVolume (name)
1. `name {string}`
2. Return: `{number}`

Returns the volume level of the specified sound.

~~~
audiomanager.getVolume('levelmusic'); //=> 0.8
~~~

### audiomanager.setMuted (isMuted)
1. `isMuted {boolean}`

Mute volume on all sounds.

### audiomanager.getMuted ()
1. Return: `{boolean}`

Check the mute status of all sounds.

### audiomanager.setMusicMuted (isMuted)
1. `isMuted {boolean}`

Mute volume on music sound.

### audiomanager.getMusicMuted ()
1. Return: `{boolean}`

Check the mute status of the music sound.

### audiomanager.setEffectsMuted (areEffectsMuted)
1. `areEffectsMuted {}`

Mute volume on effects sounds.

### audiomanager.getEffectsMuted ()
1. Return: `{boolean}`

Check the mute status of the effects sounds.

### audiomanager.setPath (path)
1. `path {string}`

Set a new path for the sound group.

~~~
audiomanager.setPath('resources/sounds/music');
~~~

### audiomanager.getPath ([name])
1. `name {string}` ---Optional sound name.
2. Return: `{string}`

~~~
audiomanager.getPath();        //=> "resources/sounds"
audiomanager.getPath('boink'); //=> "resources/sounds/effect"
~~~

### audiomanager.getExt ()
1. Return `{string}`

Returns the file extenstion of the sound.

~~~
audiomanager.getExt() //=> ".mp3"
~~~