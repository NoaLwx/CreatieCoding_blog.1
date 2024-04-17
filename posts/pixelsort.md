---
title: Pixel Sort
published_at: 2024-04-16
snippet: Glitch Art
disable_html_sanitization: true
---

## Pixel sort

<canvas id="pixel_sort"></canvas>

<script type="module">
  import { PixelSorter } from "/scripts/pixel_sort.js";

  const cnv = document.getElementById(`pixel_sort`);
  cnv.width = cnv.parentNode.scrollWidth;
  cnv.height = (cnv.width * 9) / 16;

  const ctx = cnv.getContext(`2d`);

  //load the function in
  const sorter = new PixelSorter(ctx);

  //load the image in
  const img = new Image();
  img.onload = () => {
    cnv.height = cnv.width * (img.height / img.width);
    ctx.drawImage(img, 0, 0, cnv.width, cnv.height);
    sorter.init();
    draw_frame();
  };

  //image source
  img.src = `/w5/cat.jpg`;

  //start to draw the image from zero (nothing) to a defined size
  let frame_count = 0;
  const draw_frame = () => {
    ctx.drawImage(img, 0, 0, cnv.width, cnv.height);

    let sig = Math.cos((frame_count * 2 * Math.PI) / 500);

    //size is half the width and half the height of the image
    const mid = {
      x: cnv.width / 2,
      y: cnv.height / 2,
    };
    //dimension of the pixelsorter getting bigger and bigger
    const dim = {
      x: Math.floor((sig + 3) * (cnv.width / 6)) + 1,
      y: Math.floor((sig + 1) * (cnv.height / 6)) + 1,
    };
    //
    const pos = {
      x: Math.floor(mid.x - dim.x / 2),
      y: Math.floor(mid.y - dim.y / 2),
    };

    sorter.glitch(pos, dim);

    frame_count++;
    requestAnimationFrame(draw_frame);
  };
</script>
