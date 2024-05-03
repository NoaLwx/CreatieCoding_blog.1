---
title: WEEK 4
published_at: 2024-04-9
snippet: Canvas API
disable_html_sanitization: true
---

# Canvas API

Canvas API is different to p5.js, in a lot of way. So I encountered a bit of problem first time using it.

Different from p5, I have to create a separate canvas in the html code and then calling it by using getElementById. And the fillStyle and how to draw is different too.

Canvas API in my opinion is a bit harder than p5.js, it's less straightforward and requires more codes.

But anyway, I made the square move!

## Making the things move

<canvas id="canvas"></canvas>

<script type="module">
const cnv  = document.getElementById ('canvas')
cnv.width = 400
cnv.height = 400
const ctx = cnv.getContext ('2d')

ctx.fillStyle = `pink`
ctx.fillRect (0, 0, cnv.width, cnv.height)

let x_pos = -100
requestAnimationFrame (draw_frame)

function draw_frame() {
ctx.fillStyle = `pink`
ctx.fillRect (0,0, cnv.width,cnv.height)

ctx.fillStyle = `red`
ctx.fillRect (x_pos,150,100,100)

x_pos += 1

if (x_pos > 400){
    x_pos = -100
}
requestAnimationFrame (draw_frame)
}
</script>

This is not that much different from how to make a square move in p5.js. It's still have the same principle, just a different way of coding. Afterall, p5.js is also a javascript base program.

## Clicking

<canvas id="onclick_example"></canvas>

<script type="module">
    const cnv = document.getElementById (`onclick_example`)
    cnv.width = cnv.parentNode.scrollWidth
    cnv.height = cnv.width * 9 / 16
    const coordinates = []


    function add_coordinate (e) {
        coordinates.push ({
            x : e.offsetX,
            y : e.offsetY
        })
    }

    cnv.onclick = add_coordinate
    const ctx = cnv.getContext ('2d')    

  
    function draw_frame () {

        ctx.fillStyle = `orange`
        ctx.fillRect (0, 0, cnv.width, cnv.height)
        ctx.fillStyle = `black`

        coordinates.forEach (p => {

            ctx.fillRect (p.x - 10, p.y - 10, 20, 20)
        })
        requestAnimationFrame (draw_frame)
    }
    requestAnimationFrame (draw_frame)
</script>

I started to experiment around with different function on Canvas API. For this, I tried doing the drawing with square by clicking. On p5.js, it was much easier with mouseX and mouseY. However, on Canvas API, they need the code named 'event' (or e for short) to locate the position of the mouse pointer.

This also is defined in a separate function, rather than combining with the draw function like in p5.

## Recursion

This is a total ripoff of Thomas' blog. I was trying to do it myself but I couldn't so I got Thomas' code. The only thing I changed were the variables. This made it not a tree anymore but more like a gem/beehive.

I put the vector class file on a different file and then called it here using script.

<canvas id='fractal_tree_1'></canvas>

<script src="/w4/vector.js"></script>

<script type="module">
    const cnv = document.getElementById ('fractal_tree_1')
    cnv.width = cnv.parentNode.scrollWidth
    cnv.height = cnv.width * 9 / 16

    const ctx = cnv.getContext ('2d')

    // define a function to return a random value
    // between a minimum and maximum
    function rand_between (min, max) {
        const dif = max - min
        const off = Math.random () * dif
        return  min + off
    }

    // this function has been modified to recieve 
    // an options object housing angle and mult data
    function tree (base, stem, generation, options) {
        const end = base.clone ()
        end.add (stem)

        ctx.beginPath ()
        ctx.moveTo (base.x, base.y)
        ctx.lineTo (end.x, end.y)
        ctx.stroke ()


        if (generation > 0) {
            const L_stem = stem.clone ()

            // use the data in the options object
            // for the left angle
            L_stem.rotate (options.angle.l)

            // for the left multiplier
            L_stem.mult (options.mult.l)

            const R_stem = stem.clone ()

            // for the right angle
            R_stem.rotate (options.angle.r)

            // and for the right multiplier
            R_stem.mult (options.mult.r)

            const next_gen = generation - 1

            // pass the options object
            // on to the next generation
            tree (end, L_stem, next_gen, options)
            tree (end, R_stem, next_gen, options)
        }
    }

    const seed = new Vector (cnv.width / 2, cnv.height)
    const shoot = new Vector (0, -150)

    // function for a new tree
    function new_tree () {

        // clear the canvas
        ctx.fillStyle = `white`
        ctx.fillRect (0, 0, cnv.width, cnv.height)

        // create an options object
        // using object literal notation
        const options = {
            mult : {
                l : rand_between (1, 2),
                r : rand_between (0.5, 1),
            },

            angle : {
                l : rand_between (TAU / 12, TAU / 4) * -1,
                r : rand_between (TAU / 12, TAU / 4),
            }
        }

        // grow a tree using the options generated
        tree (seed, shoot, 8, options)
    }

    // assign the new_tree function to the 
    // .onclick property of the canvas
    cnv.onclick = new_tree

    // make a tree
    new_tree ()
</script>
