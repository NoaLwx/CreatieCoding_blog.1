---
title: WEEK 7 Audio
published_at: 2024-04-24
snippet: Adding audio
disable_html_sanitization: true
---

initialise audio context so that it won't blast you with sound when you open it.

<canvas id="rapid_notes"></canvas>

<script type="module">

const cnv = document.getElementById (`rapid_notes`)
cnv.width = cnv.parentNode.scrollWidth;
cnv.height = cnv.width * 9 / 16;
cnv.style.backgroundColor = 'orange';

const audio_context = new AudioContext ()

function init_audio() {
    if (!audio_context) {
        audio_context = new (window.AudioContext || window.webkitAudioContext)();
    }
}


// array of notes for the sounds
const notes = [ 69, 73, 76 ]

// declaring a mutable iterator
let i = 0

// declaring a mutable state value
let running = false

// declaring a mutable variable for 
// the period of time between notes
let period = 200

// declaring a mutable variable for
// the length of the note
let len = 0

function play_note (note, length) {

    // if the audio context is not running, resume it
    if (audio_context.state != 'running') init_audio ()

    // create an oscillator
    const osc = audio_context.createOscillator ()

    // make it a triangle wave this time
    osc.type = 'triangle'

    // set the value using the equation 
    // for midi note to Hz
    osc.frequency.value = 440 * 2 ** ((note - 69) / 12)

    // create an amp node
    const amp = audio_context.createGain ()

    // connect the oscillator 
    // to the amp
    // to the audio out
    osc.connect (amp).connect (audio_context.destination)

    // the .currentTime property of the audio context
    // contains a time value in seconds
    const now = audio_context.currentTime

    // make a gain envelope
    // start at 0
    amp.gain.setValueAtTime (0, now)

    // take 0.02 seconds to go to 0.4, linearly
    amp.gain.linearRampToValueAtTime (0.4, now + 0.02)

    // this method does not like going to all the way to 0
    // so take length seconds to go to 0.0001, exponentially
    amp.gain.exponentialRampToValueAtTime (0.0001, now + length)

    // start the oscillator now
    osc.start (now)

    // stop the oscillator 1 second from now
    osc.stop  (now + length)
}

// declaring a function that plays the next note
function next_note () {

    // use the iterator to select a note from 
    // the notes array and pass it to the 
    // play_note function along with the 
    // len variable to specify the length of the note
    play_note (notes[i], len)

    // iterate the iterator
    i++

    // if i gets too big
    // cycle back to 0
    i %= notes.length
}

// this is a recursive function
function note_player () {

    // play the next note
    next_note ()

    // if running is true
    // it uses setTimeout to call itself 
    // after period milliseconds
    if (running) setTimeout (note_player, period)
}

// this function handles the mouse event
// when the cursor enters the canvas
cnv.onpointerenter = e => {

    // set running to true
    running = true;

    // initiate the recurseive note_player function
    note_player ()
}

// this function handles the mouse event
// when the cursor moves over the canvas
cnv.onpointermove = e => {

    // as the cursor goes from left to right
    // len gos from 0 to 5
    len = 2 * e.offsetX / cnv.width

    // as the cursor goes from bottom to top
    // period goes from 420 to 20 (milliseconds)
    period = 20 + ((e.offsetY / cnv.height) ** 2) * 40
}

// this function handles the mouse event
// when the cursor leaves the canvas
cnv.onpointerleave = e => {

    // set running to false
    running = false
}

</script>
