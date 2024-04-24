---
title: WEEK 6 ASCII
published_at: 2024-04-17
snippet: ASCII Camera
disable_html_sanitization: true
---

<div id="ascii_div"></div>

<script type="module">

    // wait for navigator media to happen then execute the code
    // get camera stream, with options
   const stream = await navigator.mediaDevices.getUserMedia ({ 

    // no audio
      audio: false,
    // allow visual
      video: true,
    // 
      facingMode: `user`,
   })

    // get video track
   const videoTracks = await stream.getVideoTracks ()
   console.log (`Using video device: ${ videoTracks[0].label }`)
    
    // make video html element
   const video = document.createElement (`video`)

    //assign stream to video source
   video.srcObject = stream
   await video.play ()

    // make canvas html element
   const cnv = document.createElement (`canvas`)

   // small size
   cnv.width  = 64
   // with aspect ratio from video html element
   cnv.height = cnv.width * video.videoHeight / video.videoWidth

    // grab the ascii from DOM
   const div = document.getElementById (`ascii_div`)

    // get font to be monospace
  div.style.fontFamily = `monospace`
    //center aligned
  div.style.textAlign = `center`

    // get canvas context
   const ctx = cnv.getContext (`2d`)

    // different characters for the input
    //string of characters from darkest to lightess
    const chars = "⠿⠾⠽⠼⠼⠼⠹⠸⠷⠶⠵⠴⠴⠲⠱⠰⠯⠮⠭⠬⠄⠃⠂⠁⠀"
    // const chars = "mwpqhsaekodcli."

    //getting a function for animation
   const draw_frame = async () => {

    // flipping the image around -> mirror/webcame
    //transformation save point
      ctx.save ()
      // flip horizontally
      ctx.scale (-1, 1)
      // draw image from video onto wrong side
      ctx.drawImage (video, -cnv.width, 0, cnv.width, cnv.height)
      //flip it back
      ctx.restore ()

    // get pixel data
      const pixels = await ctx.getImageData (0, 0, cnv.width, cnv.height).data
    //start empty string
      let ascii_img = ``

    // getting data to transform into the ascii
    // skipping each second line becuz characters are taller than a pixel
      for (let y = 0; y < cnv.height; y += 2) {
         for (let x = 0; x < cnv.width; x++) {
              // get pixel position
            const i = (y * cnv.width + x) * 4 // each pixel has 4 position (rgba)

              // get rgb value
            const r = pixels[i]
            const g = pixels[i + 1]
            const b = pixels[i + 2]

              // calculate brightness
            const br = (r * g * b / 16581375) ** 0.1

              // use brightness to select character
            const char_i = Math.floor (br * chars.length)

              // add character to ascii string
            ascii_img += chars[char_i]
         }

         // shifting the character into a new line
         ascii_img += `\n`
      }

      div.innerText = ascii_img

      requestAnimationFrame (draw_frame)
   }

   draw_frame ()
</script>
