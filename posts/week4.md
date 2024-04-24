---
title: WEEK 4
published_at: 2024-04-9
snippet: Canvas API
disable_html_sanitization: true
---

# Canvas API

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
