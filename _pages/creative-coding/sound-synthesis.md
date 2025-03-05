---
title: Sound Synthesis
---
{% assign lvl = page.url | append:'X' | split:'/' | size %}
{% capture relative %}{% for i in (3..lvl) %}../{% endfor %}{% endcapture %}

To use the sound library, we have to include the [p5.sound library](https://p5js.org/reference/p5.sound/) in our project's `index.html` file after the p5.js file, like this:

```html
<script src="https://cdn.jsdelivr.net/npm/p5@1.11.1/lib/p5.js"></script>
<script src="https://cdn.jsdelivr.net/npm/p5@1.11.1/lib/addons/p5.sound.js"></script>
```

## Oscillators

There are four types of basic oscillators, as can be seen below.

<div class="scaled-images left">
  <img src="{{ relative }}/assets/images/creative-coding/sound-synthesis-00.jpg"/>
</div>

Each oscillator has a type, a frequency and an amplitude for its wave.

<div class="scaled-images left">
  <img src="{{ relative }}/assets/images/creative-coding/sound-synthesis-01.jpg"/>
</div>

This sketch allows us to switch between the oscillator types, while adjust the frequency and amplitude of the wave
with the mouse.

{% include p5-editor-dh.html id="HsN-4i1qR" %}


One common technique in sound synthesis is to use a second wave to modulate (change) the amplitude of the first wave.

<div class="scaled-images left">
  <img src="{{ relative }}/assets/images/creative-coding/sound-synthesis-02.jpg"/>
</div>

This sketch uses the mouse to control the frequencies of the two waves
 (the 2nd controlling the amplitude of the first).

{% include p5-editor.html id="QcdtusOiTL" %}

We can also use a 2nd wave to modulate the frequency of the first wave.

<div class="scaled-images left">
  <img src="{{ relative }}/assets/images/creative-coding/sound-synthesis-03.jpg"/>
</div>

Here we use the mouse to control the amplitude and frequency of the 2nd wave, 
which controls the frequency of the first.

{% include p5-editor.html id="KyShmYHvS" %}

## Simple Synth

We can create a simple synth from oscillators by mapping different frequencies to keys.

{% include p5-editor.html id="75x3A-SAd" %}


Or we can use MIDI notes to do the same.

{% include p5-editor-dh.html id="A4ytNn90o" %}

## Attack, Decay, Sustain, Release

We can shape our notes by creating an *envelope*.

<div class="scaled-images left">
  <img src="{{ relative }}/assets/images/creative-coding/sound-synthesis-04.jpg"/>
</div>

<div class="scaled-images left">
  <img src="{{ relative }}/assets/images/creative-coding/sound-synthesis-05.jpg"/>
</div>

This sketch adds a p5.Envelope object to our sketch to control the attack, decay, sustain and release
of our notes.

{% include p5-editor.html id="GjbUx3543" %}

## Generative Audio

This gives us the basic techniques with which to synthesize generative audio.

Here is an example of putting it all together (Oscillators, Envelopes, Reverb, MIDI & an FFT) using an L-System to select the notes.

{% include p5-editor-dh.html id="CthXF6VcR" %}
