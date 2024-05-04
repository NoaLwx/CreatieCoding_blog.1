---
title: WEEK 6 Example 1
published_at: 2024-04-17
snippet: c2.js example
disable_html_sanitization: true
---

<script src="/script/c2.js"></script>
<!-- <script src="/script/p5.min.js"></script> -->

<canvas id="c2"></canvas>

Code from [here](https://c2js.org/examples.html?name=Delaunay)

<script>
const renderer = new c2.Renderer(document.getElementById('c2'));
resize();

renderer.background('#cccccc');
let random = new c2.Random();


class Agent extends c2.Point {
    constructor() {
        let x = random.next(renderer.width);
        let y = random.next(renderer.height);
        super(x, y);

        this.vx = random.next(-2, 2);
        this.vy = random.next(-2, 2);
    }

    update() {
        this.x += this.vx;
        this.y += this.vy;

        if (this.x < 0) {
            this.x = 0;
            this.vx *= -1;
        } else if (this.x > renderer.width) {
            this.x = renderer.width;
            this.vx *= -1;
        }
        if (this.y < 0) {
            this.y = 0;
            this.vy *= -1;
        } else if (this.y > renderer.height) {
            this.y = renderer.height;
            this.vy *= -1;
        }
    }

    display() {
        renderer.stroke('#333333');
        renderer.lineWidth(5);
        renderer.point(this.x, this.y);
    }
}

let agents = new Array(20);
for (let i = 0; i < agents.length; i++) agents[i] = new Agent();


renderer.draw(() => {
    renderer.clear();

    let delaunay = new c2.Delaunay();
    delaunay.compute(agents);
    let vertices = delaunay.vertices;
    let edges = delaunay.edges;
    let triangles = delaunay.triangles;

    let maxArea = 0;
    let minArea = Number.POSITIVE_INFINITY;
    for (let i = 0; i < triangles.length; i++) {
        let area = triangles[i].area();
        if(area < minArea) minArea = area;
        if(area > maxArea) maxArea = area;
    }

    renderer.stroke('#333333');
    renderer.lineWidth(1);
    for (let i = 0; i < triangles.length; i++) {
        let t = c2.norm(triangles[i].area(), minArea, maxArea);
        let color = c2.Color.hsl(30*t, 30+30*t, 20+80*t);
        renderer.fill(color);
        renderer.triangle(triangles[i]);
    }
    

    for (let i = 0; i < agents.length; i++) {
        agents[i].display();
        agents[i].update();
    }
});


window.addEventListener('resize', resize);
function resize() {
    let parent = renderer.canvas.parentElement;
    renderer.size(parent.clientWidth, parent.clientWidth / 16 * 9);
}
</script>

```javascript

<script type="module">

// loading the new renderer
const renderer = new c2.Renderer(document.getElementById('c2'));

// resize the renderer
resize();

// adding background to the canvas
renderer.background('#cccccc');

// define the new random function
let random = new c2.Random();

// define a new class
class Agent extends c2.Point {
    // setting the variable for the class
    constructor() {
        let x = random.next(renderer.width);
        let y = random.next(renderer.height);
        super(x, y);

        this.vx = random.next(-2, 2);
        this.vy = random.next(-2, 2);
    }

    // define a function for update
    // this function will create a new variable each time it moves
    update() {
        this.x += this.vx;
        this.y += this.vy;

        // if it touches the left corner of the canvas,
        // moves in the opposite dirrection
        if (this.x < 0) {
            this.x = 0;
            this.vx *= -1;
        // similarly, if it touches the right corner of the canvas
        // moves in the opposite direction
        } else if (this.x > renderer.width) {
            this.x = renderer.width;
            this.vx *= -1;
        }

        // if it touches the top of the canvas,
        // moves in the opposite direction
        if (this.y < 0) {
            this.y = 0;
            this.vy *= -1;

        // if it touches the bottom of the canvas,
        // moves in the opposite direction
        } else if (this.y > renderer.height) {
            this.y = renderer.height;
            this.vy *= -1;
        }
    }

    // draw the stroke
    display() {
        renderer.stroke('#333333');
        renderer.lineWidth(5);
        renderer.point(this.x, this.y);
    }
}

// creating an array for the points
let agents = new Array(20);
for (let i = 0; i < agents.length; i++) agents[i] = new Agent();

// draw the function
renderer.draw(() => {

    // clear existing functions
    renderer.clear();

    // define new variables of delaunay
    let delaunay = new c2.Delaunay();
    delaunay.compute(agents);
    let vertices = delaunay.vertices;
    let edges = delaunay.edges;
    let triangles = delaunay.triangles;

    let maxArea = 0;
    let minArea = Number.POSITIVE_INFINITY;

    for (let i = 0; i < triangles.length; i++) {
        let area = triangles[i].area();
        if(area < minArea) minArea = area;
        if(area > maxArea) maxArea = area;
    }


    renderer.stroke('#333333');
    renderer.lineWidth(1);
    for (let i = 0; i < triangles.length; i++) {
        let t = c2.norm(triangles[i].area(), minArea, maxArea);
        let color = c2.Color.hsl(30*t, 30+30*t, 20+80*t);
        renderer.fill(color);
        renderer.triangle(triangles[i]);
    }


    for (let i = 0; i < agents.length; i++) {
        agents[i].display();
        agents[i].update();
    }
});

// add event function for resizing
window.addEventListener('resize', resize);

// define the resizing of the canvas
function resize() {
    let parent = renderer.canvas.parentElement;
    renderer.size(parent.clientWidth, parent.clientWidth / 16 * 9);
}
</script>
```
