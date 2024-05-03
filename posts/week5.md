---
title: WEEK 5
published_at: 2024-04-16
snippet: Glitch Art
disable_html_sanitization: true
---

# Glitch Art - When imperfection became art

## Which of Ngai's aesthetic categories does your self-portrait (and glitch more generally) belong to, and why?

Glitch art is chaos and zany.

Zany is chaos, something unpredictable and often messes up the existing things. It's hysteria and maniac, though, still have a charm to its own aesthetic.

Zany is crazy, zany is unexpected, zany can be absurb, eccentric, different. You never know what is the next move of the chaos, since they always changing and creating new things.

In digital world, glitch is zany. We don't want it to happen, we don't want a scanned file to have a unexpexted object in it, we don't want a corrupted, pixelated photo, we don't want unreadable data.

But, people have found a way to enjoy the chaos, turned the unpexpected error into some form of art, **glitch art**. It's the art of chaos, the art of unexpected, and with moderation, it was turned into something beautiful, aesthetic, rather than just being an error.

## Does glitch increase or decrease effective complexity, and why?

Glitch often doesn't follow a rule. And while effective complexity although looks similar to chaos, actually does follow a rule.

Glitch decreases the effective complexity because it's no longer comprehensive. Everything about glitch is random, it advert the expectation of the user/audience, therefore, it's chaotic.

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
  //gabbing the canvas element from the document
  const cnv = document.getElementById(`glitch_self_portrait`);

  //sizing it to have a nice size
  cnv.width = cnv.parentNode.scrollWidth;
  cnv.height = (cnv.width * 9) / 16;

  //setting the background colour
  cnv.style.backgroundColor = `deeppink`;

  //getting canvas context
  const ctx = cnv.getContext(`2d`);

  //instatiating variable for img_data
  let img_data;

  //defining a function that draws the image to the canvas. Arrow is a defining a function.
  const draw = (i) => ctx.drawImage(i, 0, 0, cnv.width, cnv.height);

  //creating a new image element
  const img = new Image();

  //defining function to execute upon loading image file
  img.onload = () => {
    //resizing the height of the canvas
    cnv.height = cnv.width * (img.height / img.width);

    // drawing the image
    draw(img);

    // storing the image data as a string in img_data
    img_data = cnv.toDataURL("image/jpeg");

    // call the glitch function
    add_glitch();
  };

  // give filepath to image element
  img.src = `/w5/cat.jpg`;

  // defining a function that returns a random value
  //that is an integer between the zero and the max
  const rand_int = (max) => Math.floor(Math.random() * max);

  // defining  a recursive function, taking the data as a string
  const glitchify = (data, chunk_max, repeats) => {
    // random multiple of 4 between 0 and chunk_max
    const chunk_size = rand_int(chunk_max / 4) * 4;

    // random position in the data between 24 and chunk_size
    const i = rand_int(data.length - 24 - chunk_size) + 24;

    // grabbing all the data before the random position
    const front = data.slice(0, i);

    // leaving a gap the size of chunk_size
    // grabbing the rest of the data
    const back = data.slice(i + chunk_size, data.length);

    // putting the two pieces back together
    // leaving out a chunk
    const result = front + back;

    // ternary operator (condition ? exprIfTrue : exprIfFalse).
    //if this is = 0 -> return the first variable
    //otherwise call itself again with the repeat
    return repeats == 0 ? result : glitchify(result, chunk_max, repeats - 1);
  };

  // instatiating an empty array
  const glitch_arr = [];

  // defining function that adds a glitch image
  // to the glitch_arr array
  const add_glitch = () => {
    //make new image element
    const i = new Image();

    // define function that execute when image recieves its data
    i.onload = () => {
      // push the image into the glitch_arr array
      glitch_arr.push(i);

      // call itself until there are 12 glitched images
      if (glitch_arr.length < 12) add_glitch();
      //once there is 12 images, start animating
      else draw_frame();
    };

    //max_chunk is 96, and leaving 6 gaps
    i.src = glitchify(img_data, 96, 6);
  };

  // instantiate variable to keep track of the glitch state
  let is_glitching = false;

  // keep track of whihc glitch image from the array we are using
  let glitch_i = 0;

  const draw_frame = () => {
    // check to see if we are glitching
    // if so, draw the glitch image from the array
    if (is_glitching) draw(glitch_arr[glitch_i]);
    // otherwise draw the regular image
    else draw(img);

    // probability weightings for starting and stopping the glitch
    const prob = is_glitching ? 0.05 : 0.02;

    // if random is less than weight value
    if (Math.random() < prob) {
      // choose a random glitch image index
      glitch_i = rand_int(glitch_arr.length);

      //flip the state of is_glitching
      is_glitching = !is_glitching;
    }

    // call the next animation frame
    requestAnimationFrame(draw_frame);
  };
</script>
```

---

<canvas id="pixel_sort"></canvas>

<script type="module">
  import { PixelSorter } from "/script/pixel_sort.js";
 
  const cnv = document.getElementById(`pixel_sort`);
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

  img.src = `/w5/427.jpg`;

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

```html
<script type="module">
  import { PixelSorter } from "/script/pixel_sort.js";

  // grabbing the canvas element from the document
  const cnv = document.getElementById(`pixel_sort`);

  // sixing the canvas to have a nice size
  cnv.width = cnv.parentNode.scrollWidth;
  cnv.height = (cnv.width * 9) / 16;

  // loading the context in
  const ctx = cnv.getContext(`2d`);

  // creating a new sorter element
  const sorter = new PixelSorter(ctx);

  // load the image in
  const img = new Image();

  //defining function to execute upon loading image file
  img.onload = () => {
    // sizing the canvas to the image heigh
    cnv.height = cnv.width * (img.height / img.width);
    //sizing and placing draw function in the canvas
    ctx.drawImage(img, 0, 0, cnv.width, cnv.height);

    // calling the sorter function
    sorter.init();

    // draw image
    draw_frame();
  };

  // give filepath to image element
  img.src = `/w5/427.jpg`;

  //reseting the frame count to 0 (the start)
  let frame_count = 0;

  // start to draw frame
  const draw_frame = () => {
    // sizing and placing draw function in the canvas
    ctx.drawImage(img, 0, 0, cnv.width, cnv.height);

    //define function for sig
    let sig = Math.cos((frame_count * 2 * Math.PI) / 500);

    // sizing the sorter to half the width and half the height of the canvas
    const mid = {
      x: cnv.width / 2,
      y: cnv.height / 2,
    };

    // dimension of the pixelsorter getting bigger and bigger
    // the Math.floor function keeping the number being integer
    const dim = {
      x: Math.floor((sig + 3) * (cnv.width / 6)) + 1,
      y: Math.floor((sig + 1) * (cnv.height / 6)) + 1,
    };

    // dimension of the pixelsorter getting smaller and smaller
    const pos = {
      x: Math.floor(mid.x - dim.x / 2),
      y: Math.floor(mid.y - dim.y / 2),
    };

    // calling the sorter glitch function
    sorter.glitch(pos, dim);

    // increasing  frame
    frame_count++;

    // drawing the glitch
    requestAnimationFrame(draw_frame);
  };
</script>
```
