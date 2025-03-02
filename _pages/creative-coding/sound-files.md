---
title: Samples
---

To use the sound library, we have to include the [p5.sound library](https://p5js.org/reference/#/libraries/p5.sound) in our project's `index.html` file after the p5.js file, like this:

```html
<script src="https://cdn.jsdelivr.net/npm/p5@1.11.1/lib/p5.js"></script>
<script src="https://cdn.jsdelivr.net/npm/p5@1.11.1/lib/addons/p5.sound.js"></script>
```

## Playing Samples

First, let's load a sound sample from file using the [`loadSound()`](https://p5js.org/reference/p5/loadSound) function and test it. This is similar to how we have loaded images, text files, datasets, etc using the `preload()` function. We can use most sound formats including .wav, .aiff, .mp3 and .ogg.

The `loadSound()` function returns a [`SoundFile`](https://p5js.org/reference/p5.sound/p5.SoundFile/) object, and we can use its [`play()`](https://p5js.org/reference/p5.SoundFile/play/) function to play the song whenever we click the mouse:

{% include p5-editor.html id="aLnj1hrsv" %}

What happens if we click the mouse multiple times? It sounds like the `song` object starts playing the file multiple times over itself.

There are two ways we can fix this.

First, we can specify the file's [`playMode()`](https://p5js.org/reference/p5.SoundFile/playMode) to be either `restart` or `untilDone`, and that will make it only play one instance of the file, either by starting the song over or not doing anything until it plays until the end:

{% include p5-editor.html id="yD2bhgfPO" %}

The other way is to check first if the object is already playing the file and only call `play()` if it's not. We can also use [`isPlaying()`](https://p5js.org/reference/p5.SoundFile/isPlaying) to change the background color as an indication of the play state:

{% include p5-editor.html id="cKAbzWY2a" %}

## Visualising the sound

Let's visualise a sample while its playing.

The p5.js `SoundFile` object doesn't seem to have any function or variable that tells us the exact values of the samples that are currently playing. The closest thing it has is a [`getPeaks()`](https://p5js.org/reference/p5.SoundFile//getPeaks) function that gives us a simplified, resampled, version of values for the entire sound file.

The default length of the array returned by `getPeaks()` is $$5$$ times the canvas `width`, so no matter how long the song is, the length of the peaks array will always be the same. The numbers in this array represent samples, which are like the pixels of sound files. In this case they have been normalized to a range of $$[-1, 1]$$, where numbers with larger *absolute* values represent louder samples.

We can use this to map the sample values of the current song from $$[-1, 1]$$ to values between $$[0, width]$$ that we can use to draw a circle:

```javascript

    // map the 'value' to the size of the circle
    let size = map( abs(value), 0, 1, 0, width);

```

Now that we know how to go from a value in the peaks array to a size for our circle,  we can do this each frame. First we get the current position of the song, and then we use it to get the current value from the peaks array. Finally, we map it to our circle size as above.

```js

    // where are we in the sample?
    let position = song.currentTime() / song.duration();
    
    // get the sample value for that position
    let value = peaks[floor(position * peaks.length)];
    
    // map it to the width of the circle
    let size = map(abs(value), 0, 1, 0, width);

```

This allows to draw a circle whose size is proportional to the volume of the current sample being played:

{% include p5-editor-dh.html id="QKWgRXdN8" %}

