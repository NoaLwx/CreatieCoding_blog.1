---
title: WEEK 7 Audio
published_at: 2024-04-24
snippet: Threejs example
disable_html_sanitization: true
---

initialise audio context so that it won't blast you with sound when you open it.

<canvas id="audio"></canvas>

<script type="module">
    const cnv = document.getElementById(`audio`);
    cnv.width = cnv.parentNode.scrollWidth;
    cnv.height = (cnv.width * 9)/16;
    cnv.style.backgroundColor = 'Pink'

    const audio_context = new AudioContext ()
    audio_context.suspend ()



</script>
