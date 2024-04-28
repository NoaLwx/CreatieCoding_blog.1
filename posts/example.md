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

    let sig = Math.cos((frame_count * 2 * Math.PI) / 500);

    const mid = {
      x: cnv.width / 2,
      y: cnv.height / 2,
    };
    const dim = {
      x: Math.floor((sig + 3) * (cnv.width / 6)) + 1,
      y: Math.floor((sig + 1) * (cnv.height / 6)) + 1,
    };
    const pos = {
      x: Math.floor(mid.x - dim.x / 2),
      y: Math.floor(mid.y - dim.y / 2),
    };

    sorter.glitch(pos, dim);

    frame_count++;
    requestAnimationFrame(draw_frame);
  };
</script>
