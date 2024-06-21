---
title: Assignment 2 Prototype - WEEK 8
published_at: 2024-05-05
snippet: Prototype for assignment 2
disable_html_sanitization: true
---

Inspired by [Sabato Visconti](https://www.sabatobox.com/pixel-sorting-experiments)'s pixelsorted photos, I decided to make my own twist on it.

Heavily referencing [Happy Coding](https://happycoding.io/tutorials/p5js/images/pixel-sorter)'s tutorial, I changed it from p5.js code to Canvas API code with the help of [this Youtube](https://youtu.be/q2YHo_9Ilyk?si=zz_N1QY188j00Tlh) tutorials and Phind.

Then, I referenced the tutorial post on [Thomas's blog](https://blog.science.family/240320_web_audio_api_synths), I was able to create the audio for when the pointer is moving over the canvas.

Changing a bit of variable and trial and error using the console.log function on the web browser, I made this pixel sorter destroy function.

This time, I can manipulate the glitch myself but still shows the chaos by adverting the user's expectation of the mouse control. The pixel sorter is on a different side of the where the pointer is, making it more unexpected and more zany.

Glitch is always consider chaotic because it is not expected. Therefor I used the pixel sort function to create the zany feeling. The audio is also a nice feature on top of the glitch itself. Glitchy audio and loud sound is always considered a an error or a glitch

~~Also this is a random image I got in my laptop, please don't question it.~~

<canvas id="example"></canvas>

<script type="module">


  const cnv = document.getElementById(`example`);
  // cnv.width = 500;
  cnv.width = cnv.parentNode.scrollWidth;
  cnv.height = (cnv.width * 9) / 16;

  const ctx = cnv.getContext(`2d`);

  const img = new Image();
  img.onload = () => {
    cnv.height = cnv.width * (img.height / img.width);
    ctx.drawImage(img, 0, 0, cnv.width, cnv.height);
    window.imageData = ctx.getImageData (0, 0, cnv.width, cnv.height);
    // sortPixels();
  };


img.src = `/w5/catnada.png`;

function randNumber (min,max){
  return Math.random() * (max - min +1) + min;
}

function sortPixels(e) {
  const pixels = imageData.data;
  
  let areaX = e.clientX; // Current mouse X position
  let areaY = e.clientY; // Current mouse Y position
  let areaWidth = randNumber (20,50); // Width of the area
  let areaHeight = randNumber (100,200); // Height of the area
   
  // Calculate the start and end indices for x and y
  let startX = areaX;
  let startY = areaY - 200;
  let endX = areaX + areaWidth;
  let endY = areaY + areaHeight;

  for (let y = startY; y < endY; y++){
    for (let x = startX ; x < endX; x++){
     const index = (y * cnv.width + x) * 4;
     const brightness = pixels[index] + pixels[index + 1] + pixels[index + 2];

// Get the brightness of the pixel below
 if (y + 1 < endY) {
  const indexBelow = ((y + 1) * cnv.width + x) * 4 ;
  const brightnessBelow = pixels[indexBelow] + pixels[indexBelow + 1] + pixels[indexBelow + 2];

  if (brightness < brightnessBelow) {
      for (let i = 0; i < 3; i++) {
      const temp = pixels[index + i];
      pixels[index + i] = pixels[indexBelow + i];
      pixels[indexBelow + i] = temp;
        }
      }
    }
  }
}
 ctx.putImageData(imageData, 0, 0);
}

cnv.addEventListener('mousemove', sortPixels);

</script>
