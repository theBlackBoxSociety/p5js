<details>
<summary>Table of Contents - click to expand!</summary>

- interaction
	- mouseposition
	- mouseclick
	- key 
  - keyIsPressed
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
- Custom functions / abstractions
- Recursion??
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
}
function draw() {
  //background(50);
  stroke(255);
  ellipse(mouseX, mouseY, 20, 20);
}
```

### Mouse clicks
Another built-in variable is called `mouseIsPressed` which holds the value true if the user is currently holding down the mouse button, and false otherwise. 

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
  background(0);
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
  background(0);
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
  background(0);
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

see https://creative-coding.decontextualize.com/transformations-and-functions/

Transformations are handy and elegant techniques for changing where and how shapes get drawn to the screen. 

### Translation
In previous examples, We’ve used the concept of an “offset” variable to change where on the screen a shape gets drawn. For example, here’s a sketch that displays a rudimentary face, whose position you can change by adjusting the xoffset and yoffset variables:

## Media
see https://creative-coding.decontextualize.com/media/

## Text & Type
see https://creative-coding.decontextualize.com/text-and-type/


## Functions 

We now know how to call functions, use and create variables. We’ve also seen that functions can give us a value instead of doing something. The next section combines all of that to allow us to **create our own functions**. This will let us organise our code into smaller chunks and treat complicated tasks as a single step.    

To write your own function, you need to do 4 things:
* Write the **return type** of the function.
* Write the **name** of the function.
* Inside parenthesis **()**, list any **parameters** the function will take.
* Inside curly brackets **{}**, write **a series of steps** that will be followed whenever that function is called. This is called the body of the function.

**Return Types**
Remember that functions can either do something (like draw an ellipse or change the fill color) or give you a value (like a random value or the current time).    

*For example, the random() function gives you a float value, which you can store in a float variable. That means that the return type of the random() function is float. Compare that to the ellipse() function, which doesn’t give you a value. It wouldn’t make any sense to try to store it in a variable. We say that the return type of the ellipse() function is void, which just means that it doesn’t return anything.*

We’ll need to keep this in mind as we write our own functions. Most of the functions we write will do something instead of giving you a value, so you’ll see a lot of function return types.

Here’s a function that draws a red circle:

```javaScript
function drawRedCircle(float circleX, float circleY, float circleDiameter) {
  fill(255, 0, 0);
  ellipse(circleX, circleY, circleDiameter, circleDiameter);
}
```

This function has a void return type (which just means it does something instead of giving you a value), and takes 3 parameters: circleX, circleY, and circleDiameter. In the body of the function, it changes the fill color to red and then uses the parameters to draw a circle.

To call this function, we’d just use its name and give it parameters, exactly like we’ve been calling preexisting functions:
```javaScript
drawRedCircle(100, 200, 50);
```

This allows us to treat a task that takes multiple steps (like changing the fill color to red and drawing a circle) as a single step. As we do more complicated tasks, this becomes very useful.

**Below a more extensive example with smileys.**
```javaScript
function smiley(int x, int y, int s) {
  noFill();
  stroke(0);
  strokeWeight(s/40);
  ellipse(x, y, s, s) ; // head
  ellipse(x-s/5, y-s/5, s/5, s/5);
  ellipse(x+s/5, y-s/5, s/5, s/5);
  arc(x, y, s*0.65, s*0.65, 0, PI, OPEN);
}

function setup() {
  createCanvas(520, 400);
  background(255);
  for (int x = 20; x < width; x+=40) {
    for (int y = 20; y < height; y+=40) {
      smiley(x, y, 40);
    }
  }
  smiley(width/2, height/2, 200);
}
```

## Recursion
Recursion is a way of controlling the flow of a program with a function that calls itself. Unlike iteration, where we walk through a repeated series of commands step-by-step, recursion can create complex behaviour such as fractals that are impossible to make in another way.

A recursive function always:
1. Has a test to see if it's time to stop (otherwise it will continue forever and freeze your program!)
2. Calls itself, usually with modified data.
 
There are different ways to set a limit. You can use a variable to count the recursion depth, and stop when the depth is enough for you. You could also set a limit by drawing shapes that get smaller and smaller, and then stop when they are small enough.

```javaScript
function setup() {
  createCanvas(600, 500);
  background(255);
}

function draw() {
  noFill();
  drawCircle(width/2, height/2, width*0.75);
  noLoop();
}

function drawCircle(int x, int y, float radius) {
  ellipse(x, y, radius, radius);
  if (radius > 2) {
    radius *= 0.75;
    // The drawCircle() function is calling itself recursively.
    drawCircle(x, y, radius);
  }
}
```


```javaScript
function setup() {
  createCanvas(900, 700);
  background(255);
  noFill(); 
  stroke(0);
  strokeWeight(1);
  rectMode(CENTER);
  noLoop();
}

function draw() {
  recursion(width/2, height/2, 320);
}

// this recursion function takes 3 arguments: location (x,y) and size (s)
function recursion(float x, float y, float s) {
  // The test: ensure that size s is greater than zero
  if (s > 3) {
    // an circle / square of size (s) at (x,y)
    //ellipse(x, y, s, s);
    rect(x, y, s, s);
    // and a recursion in half size and placed on both sides of the shape
    recursion(x + (s/2), y, s*0.5);
    recursion(x - (s/2), y, s*0.5);
    // and a a third recursion in half size and placed on top of the shape
    recursion(x, y- (s/2), s*0.5);
  }
}
```
```javaScript
/*
Recursive Tree by Daniel Shiffman.
https://processing.org/examples/tree.html

Renders a simple tree-like structure via recursion. 
The branching angle is calculated as a function of the horizontal mouse location. 
Move the mouse left and right to change the angle.
*/

float theta;  
int lenght = 200;

function setup() {
  createCanvas(700, 700);
}

function draw() {
  background(0);
  frameRate(30);
  stroke(255);
  // Let's pick an angle 0 to 90 degrees based on the mouse position
  float a = (mouseX / (float) width) * 90;
  // Convert it to radians
  theta = radians(a);
  // Start the tree from the bottom of the screen
  translate(width/2,height);
  // Draw a line 120 pixels
  line(0,0,0,-200);
  // Move to the end of that line
  translate(0,-lenght);
  // Start the recursive branching!
  branch(lenght);

}

function branch(float h) {
  // Each branch will be 2/3rds the size of the previous one
  h *= 0.66;
  
  // All recursive functions must have an exit condition!!!!
  // Here, ours is when the length of the branch is 2 pixels or less
  if (h > 2) {
    pushMatrix();    // Save the current state of transformation (i.e. where are we now)
    rotate(theta);   // Rotate by theta
    line(0, 0, 0, -h);  // Draw the branch
    translate(0, -h); // Move to the end of the branch
    branch(h);       // Ok, now call myself to draw two new branches!!
    popMatrix();     // Whenever we get back here, we "pop" in order to restore the previous matrix state
    
    // Repeat the same thing, only branch off to the "left" this time!
    pushMatrix();
    rotate(-theta);
    line(0, 0, 0, -h);
    translate(0, -h);
    branch(h);
    popMatrix();
  }
}
```

see also https://natureofcode.com/book/chapter-8-fractals/
