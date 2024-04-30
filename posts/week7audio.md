---
title: WEEK 7 Audio
published_at: 2024-04-24
snippet: Adding audio
disable_html_sanitization: true
---

initialise audio context so that it won't blast you with sound when you open it.

<div id='resume_audio'></div>

<script>
    // get and format div element
    const div_0  = document.getElementById ('resume_audio')
    div_0.width  = div_0.parentNode.scrollWidth
    div_0.style.height     = `${ div_0.width * 9 / 16 }px`
    div_0.style.textAlign  = 'center'
    div_0.style.lineHeight = div_0.style.height
    div_0.style.fontSize   = '36px'
    div_0.style.fontWeight = 'bold'
    div_0.style.fontStyle  = 'italic'
    div_0.style.color      = 'white'
    div_0.style.backgroundColor = 'hotpink'

    // get and suspend audio context
    const audio_context = new AudioContext ()
    audio_context.suspend ()

    // create string with context state
    const init_msg = `audio context is ${ audio_context.state }`

    // convert string to uppercase and pass to div element
    div_0.innerText = init_msg.toUpperCase ()

    // define an async click handler function 
    async function init_audio () {

        // wait for audio context to resume
        await audio_context.resume ()

        // then set background colour
        div_0.style.backgroundColor = 'limegreen'

        // create string with new context state
        const msg = `audio context is ${ audio_context.state }`

        // unitalicise text style
        div_0.style.fontStyle  = 'normal'

        // convert to uppercase and pass to div element
        div_0.innerText = msg.toUpperCase ()
    }

    // pass anonymous function to the .onclick property
    // of the div element
    div_0.onclick = _ => {

        // if audio context is not running
        if (audio_context.state != 'running') {
            
            // call the async init audio function
            init_audio ()
        }
    }

    
</script>
<div><button id='tone_switch'></button></div>

<script>
    // get the button and store it in a variable
    const btn = document.getElementById ('tone_switch')
    btn.innerText = 'Press for tone!' // give it some text
    btn.value = 'off'                 // give it a value

    // declare a function for toggling the sound
    function toggle_sound () {

        // if button value is 'off'
        if (btn.value == 'off') {

            // set the gain to 0.3
            amp_node.gain.value = 0.3

            // set the value to 'on'
            btn.value = 'on'

            // change the text
            btn.innerText = 'Press to stop!'
        }

        // if button value is `on`
        else if (btn.value = 'on') {

            // set the gain to 0
            amp_node.gain.value = 0

            // set the value to `off`
            btn.value = 'off'

            // change the text
            btn.innerText = 'Press for tone!'
        }
    }

    // this is the click handler for the button
    // we are using arrow notation to write
    // a function with no name
    // ie. an anonymous function
    btn.onclick = () => {

        // if the audio context is still suspended
        // resume the audio context first
        if (audio_context.state != 'running') init_audio ()

        // then call the toggle sound function
        toggle_sound ()
    }
</script>

<canvas id="audio"></canvas>

<script type="module">
    const cnv = document.getElementById(`audio`);
    cnv.width = cnv.parentNode.scrollWidth;
    cnv.height = (cnv.width * 9)/16;
    cnv.style.backgroundColor = 'Pink'

    const notes = [ 62, 66, 69, 73, 74, 73, 69, 66 ]
    let i = 0

    // declaring a mutable state value
    let running = false

    // declaring a mutable variable for 
    // the period of time between notes
    let period = 200

    // declaring a mutable variable for
    // the length of the note
    let len = 0

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
    cnv_0.onpointerenter = e => {

        // set running to true
        running = true

        // initiate the recurseive note_player function
        note_player ()
    }

    // this function handles the mouse event
    // when the cursor moves over the canvas
    cnv_0.onpointermove = e => {

        // as the cursor goes from left to right
        // len gos from 0 to 5
        len = 5 * e.offsetX / cnv_0.width

        // as the cursor goes from bottom to top
        // period goes from 420 to 20 (milliseconds)
        period = 20 + ((e.offsetY / cnv_0.height) ** 2) * 400
    }

    // this function handles the mouse event
    // when the cursor leaves the canvas
    cnv_0.onpointerleave = e => {

        // set running to false
        running = false
    }

</script>
