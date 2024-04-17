---
title: Glitch
published_at: 2024-04-16
snippet: Glitch Art
disable_html_sanitization: true
---

# Glitch Art - When imperfection became art

## Glitch

<canvas id="glitch_self_portrait"></canvas>

<script type="module">
  const cnv = document.getElementById(`glitch_self_portrait`);
  cnv.width = cnv.parentNode.scrollWidth;
  cnv.height = (cnv.width * 9) / 16;
  cnv.style.backgroundColor = `deeppink`;

  const ctx = cnv.getContext(`2d`);

  let img_data;

  const draw = (i) => ctx.drawImage(i, 0, 0, cnv.width, cnv.height);

  const img = new Image();
  img.onload = () => {
    cnv.height = cnv.width * (img.height / img.width);
    draw(img);
    img_data = cnv.toDataURL("image/jpeg");
    add_glitch();
  };

  img.src = `/w5/cat.jpg`;

  const rand_int = (max) => Math.floor(Math.random() * max);

  const glitchify = (data, chunk_max, repeats) => {
    const chunk_size = rand_int(chunk_max / 4) * 4;
    const i = rand_int(data.length - 24 - chunk_size) + 24;
    const front = data.slice(0, i);
    const back = data.slice(i + chunk_size, data.length);
    const result = front + back;
    return repeats == 0 ? result : glitchify(result, chunk_max, repeats - 1);
  };

  const glitch_arr = [];

  const add_glitch = () => {
    const i = new Image();
    i.onload = () => {
      glitch_arr.push(i);
      if (glitch_arr.length < 12) add_glitch();
      else draw_frame();
    };
    i.src = glitchify(img_data, 96, 6);
  };

  let is_glitching = false;
  let glitch_i = 0;

  const draw_frame = () => {
    if (is_glitching) draw(glitch_arr[glitch_i]);
    else draw(img);

    const prob = is_glitching ? 0.05 : 0.02;
    if (Math.random() < prob) {
      glitch_i = rand_int(glitch_arr.length);
      is_glitching = !is_glitching;
    }

    requestAnimationFrame(draw_frame);
  };
</script>

```html
<script type="module">
  const cnv = document.getElementById(`glitch_self_portrait`);
  cnv.width = cnv.parentNode.scrollWidth;
  cnv.height = (cnv.width * 9) / 16;
  cnv.style.backgroundColor = `deeppink`;

  const ctx = cnv.getContext(`2d`);

  //define the image
  let img_data;

  //draw the image pixel by pixel till reaching the ful size
  const draw = (i) => ctx.drawImage(i, 0, 0, cnv.width, cnv.height);

  //load the image in to achieve the glitch
  const img = new Image();
  img.onload = () => {
    cnv.height = cnv.width * (img.height / img.width);
    draw(img);
    img_data = cnv.toDataURL("image/jpeg");
    add_glitch();
  };

  //image source
  img.src = `/w5/cat.jpg`;

  //make the variable an integer
  const rand_int = (max) => Math.floor(Math.random() * max);

  //create the glitch effect using slice to remove the pixels randomly
  const glitchify = (data, chunk_max, repeats) => {
    const chunk_size = rand_int(chunk_max / 4) * 4;
    const i = rand_int(data.length - 24 - chunk_size) + 24;
    const front = data.slice(0, i);
    const back = data.slice(i + chunk_size, data.length);
    const result = front + back;
    return repeats == 0 ? result : glitchify(result, chunk_max, repeats - 1);
  };

  //creating glitch array
  const glitch_arr = [];

  const add_glitch = () => {
    const i = new Image();
    i.onload = () => {
      glitch_arr.push(i);
      if (glitch_arr.length < 12) add_glitch();
      else draw_frame();
    };
    i.src = glitchify(img_data, 96, 6);
  };

  //if it's not glitching, draw the image normally.
  let is_glitching = false;
  let glitch_i = 0;

  const draw_frame = () => {
    if (is_glitching) draw(glitch_arr[glitch_i]);
    else draw(img);

    const prob = is_glitching ? 0.05 : 0.02;
    if (Math.random() < prob) {
      glitch_i = rand_int(glitch_arr.length);
      is_glitching = !is_glitching;
    }

    //draw function
    requestAnimationFrame(draw_frame);
  };
</script>
```
