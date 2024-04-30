---
title: Assignment 2
published_at: 2024-04-28
snippet: Threejs example
disable_html_sanitization: true
---

<canvas id="example"></canvas>

<script type="module">
 import { PixelSorter } from "/script/pixel_sort.js";

 const cnv = document.getElementById(`example`);
  cnv.width = cnv.parentNode.scrollWidth;
  cnv.height = (cnv.width * 9) / 16;

  const ctx = cnv.getContext(`2d`);

  const sorter = new PixelSorter(ctx);

  const img = new Image();
  img.onload = () => {
    cnv.height = cnv.width * (img.height / img.width);
    ctx.drawImage(img, 0, 0, cnv.width, cnv.height);
    sorter.init();
    draw_frame();
  };

  img.src = `/w5/catnada.png`;

  let frame_count = 0;
  const draw_frame = () => {
    ctx.drawImage(img, 0, 0, cnv.width, cnv.height);
  }

  palette = [
    '#264653', '#2a9d8f',
    '#e9c46a', '#f4a261',
    '#e76f51'
  ];


function draw() {
  for (let x = 0; x < width; x++) {
    const imgColor = img.get(x, y);
    const paletteColor = getPaletteColor(imgColor);
    stroke(paletteColor);
    point(x, y);
  }

}

function getPaletteColor(imgColor) {
  const imgR = red(imgColor);
  const imgG = green(imgColor);
  const imgB = blue(imgColor);

  let minDistance = 999999;
  let targetColor;

  for (const c of palette) {
    const paletteR = red(c);
    const paletteG = green(c);
    const paletteB = blue(c);

    const colorDistance =
      dist(imgR, imgG, imgB,
           paletteR, paletteG, paletteB);

    if (colorDistance < minDistance) {
      targetColor = c;
      minDistance = colorDistance;
    }
  }

  return targetColor;
  };
</script>
