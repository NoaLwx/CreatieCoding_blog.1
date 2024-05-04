---
title: WEEK 7
published_at: 2024-04-30
snippet: Combination of c2.js and ascii
disable_html_sanitization: true
---

## Combination of ascii and c2.js

<script src="/script/c2.js"></script>

<canvas id="c2"></canvas>

<div id="ascii_div"></div>

<script type="module">
const renderer = new c2.Renderer(document.getElementById('c2'));
resize();

renderer.background('#cccccc');
let random = new c2.Random();


let world = new c2.World(new c2.Rect(0, 0, renderer.width, renderer.height));

for(let i=0; i<100; i++){
  let x = random.next(renderer.width);
  let y = random.next(renderer.height);
  let p = new c2.Particle(x, y);
  p.radius = random.next(10, renderer.height/14);
  p.color = c2.Color.hsl(random.next(0, 30), random.next(30, 60), random.next(20, 100));

  world.addParticle(p);
}

let collision = new c2.Collision();
//collision.iteration(5);
world.addInteractionForce(collision);

let pointField = new c2.PointField(new c2.Point(renderer.width/2, renderer.height/2), 1);
world.addForce(pointField);

let circle = new c2.Circle(renderer.width/2, renderer.height/2, renderer.height/4);
let circleConstraint = new c2.CircleConstraint(circle);
world.addConstraint(circleConstraint);


renderer.draw(() => {
    renderer.clear();

    let mouse = renderer.mouse;
    circle.p = new c2.Point(mouse.x, mouse.y);

    renderer.stroke('#333333');
    renderer.lineWidth(1);
    renderer.lineDash([5, 5]);
    renderer.fill(false);
    renderer.circle(circle);

    world.update();

    for(let i=0; i<world.particles.length; i++){
      let p = world.particles[i];
      renderer.stroke('#333333');
      renderer.lineWidth(1);
      renderer.lineDash(false);
      renderer.fill(p.color);
      renderer.circle(p.position.x, p.position.y, p.radius);
      renderer.lineWidth(2);
      renderer.point(p.position.x, p.position.y);
    }
    

   const chars = "¶Ñ@%&∆∑∫#Wß¥$£√?!†§ºªµ¢çø∂æåπ*™≤≥≈∞~,.…_¬“‘˚`˙"

   const div = document.getElementById (`ascii_div`)
   div.style.fontFamily = `monospace`
   div.style.textAlign = `center`

      
      const w = renderer.canvas.width
      const h = renderer.canvas.height
      const pixels = renderer.context.getImageData (0, 0, w, h).data

      let ascii_img = ``

      for (let y = 0; y < renderer.canvas.height; y += 22) {
         for (let x = 0; x < renderer.canvas.width; x += 10) {
            const i = (y * renderer.canvas.width + x) * 4
            const r = pixels[i]
            const g = pixels[i + 1]
            const b = pixels[i + 2]
            const br = (r * g * b / 16581376) ** 0.1
            const char_i = Math.floor (br * chars.length)
            ascii_img += chars[char_i]
         }
         ascii_img += `\n`
      }

      div.innerText = ascii_img
});

    window.addEventListener('resize', resize);
   function resize () {
      let parent = renderer.canvas.parentElement
      renderer.size (parent.clientWidth, parent.clientWidth / 16 * 9)
   }
</script>

```javascript
<script type="module">
const renderer = new c2.Renderer(document.getElementById('c2'));
resize();

renderer.background('#cccccc');
let random = new c2.Random();


let world = new c2.World(new c2.Rect(0, 0, renderer.width, renderer.height));

for(let i=0; i<100; i++){
  let x = random.next(renderer.width);
  let y = random.next(renderer.height);
  let p = new c2.Particle(x, y);
  p.radius = random.next(10, renderer.height/14);
  p.color = c2.Color.hsl(random.next(0, 30), random.next(30, 60), random.next(20, 100));

  world.addParticle(p);
}

let collision = new c2.Collision();
//collision.iteration(5);
world.addInteractionForce(collision);

let pointField = new c2.PointField(new c2.Point(renderer.width/2, renderer.height/2), 1);
world.addForce(pointField);

let circle = new c2.Circle(renderer.width/2, renderer.height/2, renderer.height/4);
let circleConstraint = new c2.CircleConstraint(circle);
world.addConstraint(circleConstraint);


renderer.draw(() => {
    renderer.clear();

    let mouse = renderer.mouse;
    circle.p = new c2.Point(mouse.x, mouse.y);

    renderer.stroke('#333333');
    renderer.lineWidth(1);
    renderer.lineDash([5, 5]);
    renderer.fill(false);
    renderer.circle(circle);

    world.update();

    for(let i=0; i<world.particles.length; i++){
      let p = world.particles[i];
      renderer.stroke('#333333');
      renderer.lineWidth(1);
      renderer.lineDash(false);
      renderer.fill(p.color);
      renderer.circle(p.position.x, p.position.y, p.radius);
      renderer.lineWidth(2);
      renderer.point(p.position.x, p.position.y);
    }


   const chars = "¶Ñ@%&∆∑∫#Wß¥$£√?!†§ºªµ¢çø∂æåπ*™≤≥≈∞~,.…_¬“‘˚`˙"

   const div = document.getElementById (`ascii_div`)
   div.style.fontFamily = `monospace`
   div.style.textAlign = `center`


      const w = renderer.canvas.width
      const h = renderer.canvas.height
      const pixels = renderer.context.getImageData (0, 0, w, h).data

      let ascii_img = ``

      for (let y = 0; y < renderer.canvas.height; y += 22) {
         for (let x = 0; x < renderer.canvas.width; x += 10) {
            const i = (y * renderer.canvas.width + x) * 4
            const r = pixels[i]
            const g = pixels[i + 1]
            const b = pixels[i + 2]
            const br = (r * g * b / 16581376) ** 0.1
            const char_i = Math.floor (br * chars.length)
            ascii_img += chars[char_i]
         }
         ascii_img += `\n`
      }

      div.innerText = ascii_img
});

    window.addEventListener('resize', resize);
   function resize () {
      let parent = renderer.canvas.parentElement
      renderer.size (parent.clientWidth, parent.clientWidth / 16 * 9)
   }

</script>
```

## Why does combining ideas / libraries seem to make things more aesthetically chaotic?

Each idea and library has their own rules and pattern, they have their own effective complexity rules. Effective complexity is comprehence and non-redundancy, they are containble. Glitch is uncontainable.

The more function the code has, the more complex and chaotic they are, crashing with each other, creating the error, the glitch. It's like having soup and chocolate separated from each other is fine and they taste good, but if you combine them together, it's not a good dish anymore.

There for, combining ideas and library makes thing more chaotic.

However, some ideas combined together might be aesthetically pleasing despite the chaos. And a lot of people love the chaotic aspect of glitch. Althought it's might be too bright, too scary or too weird, the imperfect of the error create a really attractive aesthetic.

We do find the beauty in imperfection.
