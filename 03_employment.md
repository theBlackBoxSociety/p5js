<details>
<summary>Table of Contents - click to expand!</summary>

- interaction
	- mouseposition
	- mouseclick
	- touches
	- key
	- Event functions
- Transformations
  - scale
  - translate
  - rotate
  - push & pop
- Media
  - images (function preload!!)
  - video (files & camera)
  - sounds (extra library)
- Text & type
</details>

# P5.JS • Employment

🚧 🚧 🚧 🚧 🚧 NOT FINISHED YET 🚧 🚧 🚧 🚧 🚧

It is time for some more instantly practical knowledge. We will some some modes of interaction, the basics of visual transformations and working with media and text.

## Interaction
### Mouse position
Processing provides two special variables, mouseX and mouseY, that contain the X and Y coordinates of the mouse cursor in the current frame. Remember that the code in draw() is running over and over again, very quickly: up to sixty times per second. A bit of pre-written code that is a part of the p5.js library calls this function over and over for you, and each time it does so, it updates the mouseX and mouseY variables with the current position of the mouse cursor on the screen. These two variables together make it easy to make your sketch react to user input in the form of mouse movement.

Here’s a quick example sketch that simply draws a circle underneath the current mouse position:

```javaScript
function setup() {
  createCanvas(400, 400);
}
function draw() {
  background(50);
  noFill();
  stroke(255);
  strokeWeight(mouseX / 10);
  ellipse(200, 200, mouseY, mouseY);
}
```
  
  
### Mouse clicks
Processing includes a special built-in variable called mouseIsPressed which holds the value true if the user is currently holding the mouse, and false otherwise. You can use this to make your sketch do different things depending on whether or not the user is holding down the mouse button.

Here’s an example that displays a circle only if the mouse button is pressed:

```javaScript
function setup() {
  createCanvas(400, 400);
}
function draw() {
  background(50);
  stroke(255);
  strokeWeight(8);
  noFill();
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

### Touches
The system variable touches[] contains an array of the positions of all current touch points, relative to (0, 0) of the canvas, and IDs identifying a unique touch as it moves. 

### Key
The system variable key always contains the value of the most recent key on the keyboard that was typed.
The boolean system variable keyIsPressed is true if any key is pressed and false if no keys are pressed.

### Event functions
The mousePressed() function is called once after every time a mouse button is pressed. 
The keyPressed() function is called once every time a key is pressed. The keyCode for the key that was pressed is stored in the keyCode variable.


## Transformations

https://creative-coding.decontextualize.com/transformations-and-functions/

In this tutorial, I’m going to show you how to use transformations. This is a handy and elegant technique for changing where and how shapes get drawn to the screen. I’m also going to show you the basics of how to write functions, which is an easy way to compartmentalize and simplify your code.

Translation
In previous examples, I’ve used the concept of an “offset” variable to change where on the screen a shape gets drawn. For example, here’s a sketch that displays a rudimentary face, whose position you can change by adjusting the xoffset and yoffset variables:

## Media
https://creative-coding.decontextualize.com/media/

## Text & Type
https://creative-coding.decontextualize.com/text-and-type/
