---
title: WEEK 7 Audio
published_at: 2024-04-24
snippet: Adding audio
disable_html_sanitization: true
---

initialise audio context so that it won't blast you with sound when you open it.

<div id='resume_audio'></div>

<script type="module">
            // get and format div element
            const div_0 = document.getElementById('resume_audio')
            div_0.width = div_0.parentNode.scrollWidth
            div_0.style.height = `${div_0.width * 9 / 16}px`
            div_0.style.textAlign = 'center'
            div_0.style.lineHeight = div_0.style.height
            div_0.style.fontSize = '36px'
            div_0.style.fontWeight = 'bold'
            div_0.style.fontStyle = 'italic'
            div_0.style.color = 'white'
            div_0.style.backgroundColor = 'hotpink'
            // get and suspend audio context
            const audio_context = new AudioContext()
            audio_context.suspend()
            // create string with context state
            const init_msg = `audio context is ${audio_context.state}`
            // convert to uppercase and pass to div element
            div_0.innerText = init_msg.toUpperCase()
            // define an async click handler function 
            async function init_audio() {

                // wait for audio context to resume
                await audio_context.resume()
                // then set background colour
                div_0.style.backgroundColor = 'limegreen'
                // create string with new context state
                const msg = `audio context is ${audio_context.state}`
                // unitalicise text style
                div_0.style.fontStyle = 'normal'
                // convert to uppercase and pass to div element
                div_0.innerText = msg.toUpperCase()
            }

            // pass anonymous function to the .onclick property
            // of the div element
            div_0.onclick = _ => {

                // if audio context is not running
                if (audio_context.state != 'running') {

                    // call the async init audio function
                    init_audio()
                }
            }
</script>

<canvas id="rapid_notes"></canvas>

<script type="module">

let audio_context;

function init_audio() {
    if (!audio_context) {
        audio_context = new (window.AudioContext || window.webkitAudioContext)();
    }
}

const cnv_0 = document.getElementById (`rapid_notes`)
cnv_0.width = cnv_0.parentNode.scrollWidth;
cnv_0.height = cnv_0.width * 9 / 16;
cnv_0.style.backgroundColor = 'orange';

// Initialize audio context
init_audio();

    // making an array of midi notes
    const notes = [ 62, 66, 69, 73, 74, 73, 69, 66 ]

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

    // declaring a function that plays the next not
function play_note (note, length) {

    // if the audio context is not running, resume it
    if (audio_context.state != 'running') init_audio ()

    // create an oscillator
    const osc = audio_context.createOscillator ()

    // make it a triangle wave this time
    osc.type            = 'triangle'

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
    cnv_0.addEventListener('pointerenter', e => {
    running = true;
    note_player();
});

cnv_0.addEventListener('pointermove', e => {
    len = 5 * e.offsetX / cnv_0.width;
    period = 20 + ((e.offsetY / cnv_0.height) ** 2) * 400;
});

cnv_0.addEventListener('pointerleave', e => {
    running = false;
});
</script>
