<details>
<summary>Table of Contents - click to expand!</summary>

- Buttons & sliders 🚧
- Dom manipulation 🚧
- from p5js to web dev 🚧
	- Custom HTML & CSS
	- Multiple Sketches in a Webpage
- external libraries 🚧
	- p5.play
	- https://github.com/zenozeng/p5.js-svg
	- https://idmnyu.github.io/p5.js-speech/
	- rita
- WEBGL 🚧	
	
</details>

# P5.JS • Advanced
🚧 🚧 🚧 🚧 🚧 NOT FINISHED YET 🚧 🚧 🚧 🚧 🚧

## Buttons & Sliders
https://creative-coding.decontextualize.com/browser-controls/
https://editor.p5js.org/hendrikleper/sketches/A3eh-QRwL


```javaScript
function setup() {
  createCanvas(400, 400);
  let button = createButton('click me!');
  button.mousePressed(clickme);
  background(220);
}

function clickme() {
  background(255,0,0);
  window.alert('alert! alert! alert!')
}

function draw() {
}
```

```javaScript
let cheer;

function preload() {
  cheer = loadSound('cheer.mp3');
}

function setup() {
  createCanvas(400, 400);
  let button = createButton("play cheer!");
  button.mousePressed(playCheer)
}

function playCheer() {
  cheer.play();
}

function draw() {
  background(220);
}
```

## DOM Manipulation
https://p5js.org/examples/dom-modifying-the-dom.html
https://editor.p5js.org/PaulGSA/sketches/7zATSqCEh

## From p5js to Webdev
https://happycoding.io/tutorials/p5js/web-dev
https://www.joemckaystudio.com/multisketches/

### Custom HTML & CSS
This example uses some custom HTML and CSS alongside the sketch. The title and paragraph are HTML elements, defined in index.html. Additionally, the p5 canvas is placed in an HTML element defined by the coder, with an id called 'container'. This lets the programmer control where it appears on the page in relationship to other elements. In this particular example, this lets us put the title above the page (an h1 element) and the paragraph (a p element) below it. 
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.1.9/p5.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.1.9/addons/p5.sound.min.js"></script>
  <link rel="stylesheet" type="text/css" href="style.css">
  <meta charset="utf-8" />
</head>
<body>
  <h1>Sketch title</h1>
  <div id="container">
  <!--sketch will be inserted here, as done in setup() in sketch.js-->
  </div>
  <p>This is a paragraph element.</p>
  <script src="sketch.js"></script>
</body>

</html>
```
```CSS
html, body {
  margin: 0;
  padding: 0;
  font-family: sans-serif;
  text-align: center;
  background: white;
}
canvas {
  display: block;
  margin: auto; /* centers the canvas */
}
```
```javaScript
function setup() {
  // new: keep a variable that holds the canvas element
  let cnv = createCanvas(400, 400);
  // assign the "parent" element to ensure that the canvas
  // is added to the element named "container"
  cnv.parent('container');
}

function draw() {
  background(0);
  ellipse(mouseX, mouseY, 50, 50);
}
```

Include multiple sketches in a webpage
http://joemckaystudio.com/multisketches/

## External Libraries 🚧
	- p5.play
	- https://github.com/zenozeng/p5.js-svg
	- https://idmnyu.github.io/p5.js-speech/
	- rita



## WebGL  🚧	

https://makeyourownalgorithmicart.blogspot.com/2018/05/artificial-life-and-conways-game-of.html
https://github.com/processing/p5.js/wiki/Getting-started-with-WebGL-in-p5


```javaScript
var img;
var counter = 0;

function setup() {
  // create a WEBGL canvas
  createCanvas(800, 600, WEBGL);
  
  // create empty image and fill pixel by pixel
  img = createImage(400, 100);
  img.loadPixels();
  for(var x = 0; x < img.width; x++) {
    for(var y = 0; y < img.height; y++) {
      // use noise() values 0-255 to create greyscale pixels
      img.set(x, y, noise(x/40,y/10)*255); 
    }
  }
  img.updatePixels();
}

function draw() {
  background('white');
  
  // animate a 3-d box
  push();
  rotateX(counter);
  rotateY(counter);
  texture(img);
  box(200, 200, 200);
  pop();
  
  // increase counter which determines rotation of box
  counter += 0.01;
}
```

## Shaders
https://itp-xstory.github.io/p5js-shaders/#/
