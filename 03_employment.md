<details>
<summary>Table of Contents - click to expand!</summary>

- [Interaction](#interaction)
	- [Mouse position](#mouse-position)
	- [Mouse clicks](#mouse-clicks)
	- [Key](#key)
	- [keyIsPressed](#keyispressed)
	- [Event functions](#event-functions)
- [Transformations](#transformations)
	- [Translation](#translation)
	- [Rotation](#rotation)
	- [Scale](#scale)
	- [Order Matters](#order-matters)
	- [Push and Pop](#push-and-pop)
- [Media](#media) 🚧
	- [Images](#images)
	- [SVG](#svg)
	- [Video](#video)
	- [Sound](#sound)
- [Text & Type](#text-type) 🚧

</details>

# P5.JS • Employment

🚧 🚧 🚧 🚧 🚧 NOT FINISHED YET 🚧 🚧 🚧 🚧 🚧

In this chapter we will see some modes of interaction, the basics of visual transformations, we'll work with media and text, formulate our own functions and use them in programs that involve recursion.

## Interaction
P5.js has a lot of built-in variables that deal with interactivity. The  majority of them monitor potential mouse actions as the horizontal (x) and vertical (y) position, button pressed (or not), etc.

### Mouse position
`MouseX` and `mouseY`, contain the X and Y coordinates of the mouse cursor in the current frame.    
Remember that the code in draw() is running over and over again, very quickly. A bit of pre-written code that is a part of the p5.js library calls this function over and over for you, and each time it does so, it updates the mouseX and mouseY variables with the current position of the mouse cursor on the screen.    
These two variables together make it easy to make your sketch react to user input in the form of mouse movement.

Here’s a quick example sketch that simply draws a circle underneath the current mouse position:

```javaScript
function setup() {
  createCanvas(400, 400);
  background(50);
  stroke(255);
  strokeWeight(5);
  noFill();
}

function draw() {
  background(50);
  stroke(255);
  ellipse(mouseX - 15, mouseY, 20, 20);
  ellipse(mouseX + 15, mouseY, 20, 20);
  line(mouseX - 20, mouseY + 30, mouseX + 20, mouseY + 30);
}
```

### Mouse clicks
Another built-in variable is called `mouseIsPressed` which holds the value true if the user is currently holding down the mouse button, and false otherwise. 

Here’s an example that displays a circle only if the mouse button is pressed:
```javaScript
function setup() {
  createCanvas(400, 400);
	stroke(255);
	strokeWeight(8);
	noFill();
}
function draw() {
  background(50);
  ellipse(150, 150, 40, 40);
  ellipse(250, 150, 40, 40);
  if (mouseIsPressed) {
    rect(100, 250, 200, 50);
  }
  else {
    line(100, 275, 300, 275);
  }
}
```

### Key
The system variable `key` always contains the value of the most recent key on the keyboard that was typed.    

```javaScript
function setup() {
  createCanvas(400, 400);
  textSize(100);
}

function draw() {
  background(50);
  stroke(255);
  strokeWeight(8);
  noFill();
  ellipse(150, 150, 40, 40);
  ellipse(250, 150, 40, 40);
  rect(180, 230, 40, 40);
  noStroke();
  fill(255);
  text(key, 200, 260);
}
```

### keyIsPressed
The system variable `keyIsPressed` is a boolean, it yields true if any key is pressed and false if no keys are pressed. It can be used to check if any key is pressed!

The example bends the smiley's mouth if a key is pressed. 
```javaScript
let y = 270;

function setup() {
  createCanvas(400, 400);
  background(50);
  stroke(255);
  strokeWeight(8);
  noFill();
}

function draw() {
  background(50);
  ellipse(150, 150, 40, 40);
  ellipse(250, 150, 40, 40);
  bezier(100, 270, 150, y, 250, y, 300, 270);
  if (keyIsPressed) {
    y = 330;
  } else {
    y = 270;
  }
}
```
Note: the function [`bezier()`](https://p5js.org/reference/#/p5/bezier) draws a [Bezier curve](https://en.wikipedia.org/wiki/B%C3%A9zier_curve) on the screen. These curves are defined by a series of anchor and control points.    
bezier(x1, y1, x2, y2, x3, y3, x4, y4)    
x1 & y1 coordinates for first anchor point    
x2 & y2 coordinates for first control point    
x3 & y3 coordinates for second control point    
x4 & y4 coordinates for second anchor point     
See [this bezier curve demo](https://editor.p5js.org/allison.parrish/sketches/H1QQ3Nt67)

This second example goes a step further and only responds when the up and down arrows are pressed.
```javaScript
let y = 270;

function setup() {
  createCanvas(400, 400);
  background(50);
  stroke(255);
  strokeWeight(8);
  noFill();
}

function draw() {
  background(50);
  ellipse(150, 150, 40, 40);
  ellipse(250, 150, 40, 40);
  bezier(100, 270, 150, y, 250, y, 300, 270);
  if (keyIsPressed) {
    if (keyCode == UP_ARROW) {
      if (y > 0) {
        y -= 1;
      }
    } else if (keyCode == DOWN_ARROW) {
      if (y < height) {
        y += 1;
      }
    }
  }
}
```

### Event functions
Events (or event functions) alter the normal flow of a program when an action such as mouse movement or a key press takes place. It is a polite interruption of the normal flow of a program. 

The code inside an event function is run once each time the corresponding event occurs. For example, if a mouse button is pressed, the code inside the mousePressed() function will run once and will not run again until the button is pressed again. The keyPressed() function is called once every time a key is pressed. The keyCode for the key that was pressed is stored in the keyCode variable.

This allows data produced by the mouse and keyboard to be read independently from what is happening in the rest of the program.
 
#### The keyPressed() function
First of all, it's a function rather than a variable. This is very important, because in order to use `keyPressed()`, you actually have to add it as a function to your sketch. That means it needs to be a totally separate code block from your `draw` and `setup` functions.

```javaScript
let y = 270;

function setup() {
  createCanvas(400, 400);
  background(50);
  stroke(255);
  strokeWeight(8);
  noFill();
}

function draw() {
  background(50);
  ellipse(150, 150, 40, 40);
  ellipse(250, 150, 40, 40);
  bezier(100, 270, 150, y, 250, y, 300, 270);
}

function keyPressed() {
  if (keyCode == UP_ARROW) {
    if (y > 0) {
      y -= 1;
    }
  } else if (keyCode == DOWN_ARROW) {
    if (y < height) {
      y += 1;
    }
  }
}
```
Do you notice the difference with the keyIsPressed variable. Yes, the `keyPressed()` function is not running repeatedly when you hold the arrow keys down. You have to repeat keypresses to see any change.

See also [this tutorial](https://www.openprocessing.org/sketch/944398) on the difference between keyPressed() and keyIsPressed?


## Transformations
<sup>based on https://processing.org/tutorials/transform2d/ <br>
see also https://creative-coding.decontextualize.com/transformations-and-functions/</sup><br>
<sup>but also check https://genekogan.com/code/p5js-transformations/ !!!!!!</sup>

Transformations are handy and elegant techniques for changing where and how shapes get drawn to the screen. This tutorial will introduce you to the translate, rotate, and scale functions.

### Translation
The `translate()` function allows objects to be moved to any location within the window. The first parameter sets the x-axis offset and the second parameter sets the y-axis offset.

In previous examples, we’ve used “offset” variables to change where on the screen a shape gets drawn. This is no longer necessary now that we can do this with translate.

Let's do this in code.
```javaScript
function setup()
{
  createCanvas(200, 200);
  background(255);
  noStroke();
  // draw the original position in gray
  fill(192);
  rect(0, 0, 40, 40);
  // draw a translucent red rectangle by changing the coordinates
  fill(255, 0, 0, 128);
  rect(0+60, 0+60, 40, 40);
  // draw a translucent blue rectangle by translating the grid
  fill(0, 0, 255, 128);
  translate(65, 65);
  rect(0, 0, 40, 40);
}
```
So the above code: draws a 40 by 40 rectangle in gray at position x=0 y=0, then draws a second red rectangle and changes its coordinates tot x=60 & y=60 and last draws it again in blue by moving the grid (`translate(65, 65);`).     
The rectangles are translucent so that you see that they partially overlap. Only the method used to move them has changed. The translate(65, 65) moves the coordinate system 65 units right and 65 units down.

A second example with our smiley.
```javaScript
function setup() {
  createCanvas(400, 400);
  background(50);
  stroke(255);
  strokeWeight(4);
  noFill();
}

function draw() {
  background(50);
  translate(mouseX, mouseY);
  ellipse(-25, 0, 20, 20);
  ellipse(25, 0, 20, 20);
  bezier(-20, 25, -20, 40, 20, 40, 20, 25);
}
``` 

### Rotation
In addition to moving the grid, you can also rotate it with the `rotate()` function. This function takes one argument, which is the number of radians that you want to rotate. In p5.js, all the functions that have to do with rotation measure angles in radians rather than degrees. When you talk about angles in degrees, you say that a full circle has 360°. When you talk about angles in radians, you say that a full circle has 2π radians. 

```javaScript
function setup()
{
  createCanvas(200, 200);
  background(255);
  noStroke();
  //draw a translucent red rectangle
  fill(255, 0, 0, 128);
  rect(60, 60, 80, 80);
  //draw a translucent blue rectangle after rotating the grid
  fill(0, 0, 255, 128);
  rotate(PI/4);
  rect(60, 60, 80, 80);
}
```

Hey, what happened? How come the square got moved and cut off? The answer is: the square did not move. The grid was rotated. Here is what really happened. As you can see, on the rotated coordinate system, the square still has its upper left corner at
(60, 60).

If you want to rotate the rectangle along it's upper left corner you need to do a translate function first. 
```javaScript
function setup()
{
  createCanvas(200, 200);
  background(255);
  noStroke();
  //draw a translucent red rectangle
  fill(255, 0, 0, 128);
  rect(60, 60, 80, 80);
  //draw a translucent blue rectangle after rotating the grid
  fill(0, 0, 255, 128);
  translate(60,60);
  rotate(PI/4);
  rect(0, 0, 80, 80);
}
```

Below a sketch that generates a color wheel using the rotation function.
```javaScript
function setup() {
  createCanvas(400, 400);
  background(0);
  smooth();
  noStroke();
  colorMode(HSB, 360);
}

function draw() {
  if (frameCount % 2 == 0) {
    fill(frameCount % 360, 360, 360);
    translate(width / 2, height / 2);
    rotate(radians(frameCount % 360));
    rect(0, 0, 300, 1);
  }
}

```
Note: The sketch is using 3 new items: the [`colorMode()`](https://p5js.org/reference/#/p5/colorMode) function, the [frameCount](https://p5js.org/reference/#/p5/frameCount) system variable and % (modulo) operator.    
The first two can be found in the reference, below more about the modulo operator.

**%** or **modulo** calculates the remainder when one number is divided by another. For example, when 52 is divided by 10, the divisor (10) goes into the dividend (52) five times (5 * 10 == 50), and there is a remainder of 2 (52 - 50 == 2). Thus, 52 % 10 produces 2.

some more examples:    
```javaScript
let a = 5 % 4;            // Sets 'a' to 1
let b = 125 % 100;        // Sets 'b' to 25
let c = 285.5 % 140.0;    // Sets 'c' to 5.5 
```
Modulo is extremely useful for ensuring values stay within a boundary, such as when keeping a shape on the screen.
```javaScript
let a = 0;
function setup(){
  createCanvas(200,100);
}
function draw() {
  background(200);
  a = (a + 1) % width;  // 'a' increases between 0 and width 
  line(a, 0, a, height);
}
```

### Scale
The final coordinate system transformation is scaling, which changes the size of the grid. Take a look at this example, which draws a square, then scales the grid to twice its normal size, and draws it again.

```javaScript
function setup() {
  createCanvas(200, 200);
  background(255);
  stroke(0);
  // draw a gray rectangle
  fill(128);
  rect(20, 20, 40, 40);
  // draw a translucent red rectangle at twice the scale
  fill(255,0,0, 128);
  scale(2.0);
  rect(20, 20, 40, 40);
}
```
First, you can see that the square appears to have moved. It hasn’t, of course. Its upper left corner is still at (20, 20) on the scaled-up grid, but that point is now twice as far away from the origin as it was in the original coordinate system. You can also see that the lines are thicker. That’s no optical illusion—the lines really are twice as thick, because the coordinate system has been scaled to double its size.

There is no law saying that you have to scale the x and y dimensions equally. Try using scale(3.0, 0.5) to make the x dimension three times its normal size and the y dimension only half its normal size.

### Order Matters
When you do multiple transformations, the order makes a difference. A rotation followed by a translate followed by a scale will not give the same results as a translate followed by 
a rotate by a scale. Here is some sample code and the results.

```javaScript
function setup() {
  createCanvas(300, 300);
  background(255);
  smooth();
  // draw axes
  line(5, 5, 250, 5);
  line(5, 5, 5, 250);
  // red square
  push();
  fill(255, 0, 0);
  rotate(radians(15));
  translate(50, 50);
  scale(2.0);
  rect(0, 0, 50, 10);
  pop();
  // white square
  push();
  fill(255);
  translate(50, 50);
  rotate(radians(15));
  scale(2.0);
  rect(0, 0, 50, 10);
  pop();
}
```

### Push and Pop
What about the `[push()](https://p5js.org/reference/#/p5/push)` and `[pop()](https://p5js.org/reference/#/p5/pop)` functions above?     
push() is a built-in function that saves the current position of the coordinate system and pop() restores the coordinate system to the way it was before transformation(s).

These come from a computer concept known as a stack, which works like a springloaded tray dispenser in a cafeteria. When someone returns a tray to the stack, its weight pushes the platform down. When someone needs a tray, he takes it from the top of the stack, and the remaining trays pop up a little bit.    
In a similar manner, push() puts the current status of the coordinate system at the top of a memory area, and pop() pulls that status back out. The preceding example used push() and pop() to make sure that the coordinate system was “clean” before each part of the drawing. 

In the first examples, the push() and pop() calls were not necessary but in the previous example it was. Try the code without push() and pop(). You will see that the scale of the white square increases again.

As soon as we draw different objects with different transformations, the use of push and pop is inevitable.

## Media
see https://creative-coding.decontextualize.com/media/

In this tutorial, We will see how to load media as images, soundfiles and video into our sketches.

Before you can use an file in your code, you need to add it to your sketch.

If you’re using the p5.js web editor:    
1. Click the > button just under the play button to expand the list of files in your sketch. You should see index.html, sketch.js, and style.css.
2. Click the dropdown menu next to Sketch Files and then click Upload file.
3. In the window that pops up, drag a file or click to select a file.
4. When your file is done uploading, close the file selector window.
5. You should now see your image file in the list of Sketch Files. 
6. You can collapse the list of sketch files by clicking the < button.

If you are using an external editor: 
1. You can just copy the file in the same directory as your index.html, style.css and sketch.js files.

### Images
You can use images in PNG or JPEG format..
```javaScript
var moon;
function preload() {
  kitty = loadImage("moon.jpg");
}
function setup() {
  createCanvas(400, 400);
}
function draw() {
  background(255);
  image(kitty, mouseX, mouseY);
}
```
```javaScript
var img; //variable containing the image

function preload(){
  img = loadImage('fullmoon_sm.jpg'); 
  // we load the image using the function loadImage() inside preload()
}

function setup(){
  createCanvas(800,760);
  colorMode(HSB,1);
}

function draw(){
  background(0);
// tint(map(mouseY,0,height,0,1),map(mouseX,0,width,0,1), 1); //the function tints the image

  image(img,0,0); //we display the image at (0,0)
  //filter(INVERT); //filter the image
}
```

```javaScript
var video;

function setup(){
  createCanvas(640,480);
  video = createCapture(VIDEO);
  video.hide();
}

function draw(){
  image(video,0,0);
  filter(INVERT);
}
```

```javaScript
/*
Source  Photo Booth Draft 5 - pixelate video to canvas
by enickles
https://editor.p5js.org/enickles/sketches/HJ-43zqvf
*/
let camera;

let videoScale = 16; // 16

function setup() {
  pixelDensity(1);
  createCanvas(640, 480);
  camera = createCapture(VIDEO);
  camera.size(width / videoScale, height / videoScale);
  // camera.hide();
}

function draw() {
  background(255);

  camera.loadPixels()
  loadPixels();
  for (let y = 0; y < camera.height; y++) {
    for (let x = 0; x < camera.width; x++) {
      let index = (x + y * camera.width) * 4;
      let r = camera.pixels[index + 0];
      let g = camera.pixels[index + 1];
      let b = camera.pixels[index + 2];

      // pixels[index+0] = b;
      // pixels[index+1] = r; 
      // pixels[index+2] = g;
      // pixels[index+3] = 255;
      
      noStroke();
			fill(r, g, b);
      rect(x * videoScale, y * videoScale, videoScale, videoScale);

    }
  }
  //updatePixels();

  // displays camera
  // image(camera, 0,0, 320, 240);

}
```
```javaScript
// https://editor.p5js.org/hendrikleper/sketches/9Vc9LMeVU
// https://medium.com/@colinpatrickreid/creating-impressionistic-art-with-photography-and-p5-js-e073d794aa40
function preload() {
  img = loadImage("artbreeder1.jpeg");
}

function setup() {
  createCanvas(512, 512);
  img.loadPixels();
  for (let x = 0; x < img.width; x += 2) {
    for (let y = 0; y < img.height; y = y += 2) {
      let index = (floor(x) + floor(y) * img.width) * 4;
      red = img.pixels[index]
      blue = img.pixels[index + 1]
      green = img.pixels[index + 2]
      alpha = img.pixels[index + 3]
      //let pixel_brightness = (red + blue + green) / 3
      //fill(red, blue, green, alpha)
      //rect(x, y, 2, 2)
      strokeWeight(5 * Math.random())
      stroke(red, blue, green, alpha/(5 * Math.random()))
      line(x + Math.random() * 40,y ,x + 50,y + 50 * Math.random())
    }
  }
}
```


### SVG
https://makeyourownalgorithmicart.blogspot.com/2018/03/creating-svg-with-p5js.html

samples
see https://editor.p5js.org/PaulGSA/sketches/ZqjKCmILU
https://editor.p5js.org/PaulGSA/sketches/-iEVohzim

### Video
https://creative-coding.decontextualize.com/video/

### Sound

## Text & Type
see https://creative-coding.decontextualize.com/text-and-type/
