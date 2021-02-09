<details>
<summary>Table of Contents - click to expand!</summary>


- Arrays

- Objects 
https://gokcetaskan.com/artofcode/classes

- Buttons & sliders
- more on sound (Synthesizing and analyzing sound)

</details>

# P5.JS • Advanced

🚧 🚧 🚧 🚧 🚧 NOT FINISHED YET 🚧 🚧 🚧 🚧 🚧

Arrays
Array is a list-like object (data structure) that contains other elements. In JavaScript, neither the length nor the types of its elements are fixed. An array's length can change at any time. Arrays use integers as element indexes.
Adopted from MDN web docs

How to define arrays?

// An empty array
let sampleList = [];

// Array with number
let randomNumbers = [3, 5, 6, 8, 10, 45, 567];

// Array with strings
let names = ["Sophia", "Charlotte", "William", "Oliver"];

// Mixed array
let everything = [6, "Sophia", 475, 67, 32, 4, "Oliver", 837];
How to modify arrays? Add, remove elements...

let arr = [];

// Print the length of the array
print(arr.length);

// Add an element
arr.push(3);

// Remove last element
arr.pop();

// Remove first element
arr.shift();
Functions
"...a sequence of program instructions that performs a specific task"
Wikipedia

p5.js comes with a lot of pre-defined functions that you can use to execute specific tasks (draw a shape, show an image, play audio...) You can also define your functions to make it easy to perform repetitive tasks.

// Define a function named myFunction
function myFunction() {
  // Instructions to be executed when function is called
  // goes inside curly braces
}

// Define setup() and call our function inside
function setup() {
  myFunction();
}
Optionally, functions can have parameters. Parameters are variables that are scoped to the function, that can be assigned a value when calling the function. — p5.js docs

function drawYellowCircle(x, y, size) {
  fill(255, 255, 0);
  circle(x, y, size);
}

drawYellowCircle(5, 10, 30);
Functions can also return a value:

// It is not useful to write a function
// for a basic arithmetic operation
// but it works well as a simple example :)

function add(value1, value2) {
  return value1 + value2;
}

let result = add(3, 9);

print(result);
// prints 12 to the console.


## <a name="functions">21 Functions</a>  

We now know how to call functions, use and create variables. We’ve also seen that functions can give us a value instead of doing something. The next section combines all of that to allow us to **create our own functions**. This will let us organise our code into smaller chunks and treat complicated tasks as a single step.    

To write your own function, you need to do 4 things:
* Write the **return type** of the function.
* Write the **name** of the function.
* Inside parenthesis **()**, list any **parameters** the function will take.
* Inside curly brackets **{}**, write **a series of steps** that will be followed whenever that function is called. This is called the body of the function.

**Return Types**
Remember that functions can either do something (like draw an ellipse or change the fill color) or give you a value (like a random value or the current time).    

*For example, the random() function gives you a float value, which you can store in a float variable. That means that the return type of the random() function is float. Compare that to the ellipse() function, which doesn’t give you a value. It wouldn’t make any sense to try to store it in a variable. We say that the return type of the ellipse() function is void, which just means that it doesn’t return anything.*

We’ll need to keep this in mind as we write our own functions. Most of the functions we write will do something instead of giving you a value, so you’ll see a lot of void return types.

Here’s a function that draws a red circle:

```java
void drawRedCircle(float circleX, float circleY, float circleDiameter) {
  fill(255, 0, 0);
  ellipse(circleX, circleY, circleDiameter, circleDiameter);
}
```

This function has a void return type (which just means it does something instead of giving you a value), and takes 3 parameters: circleX, circleY, and circleDiameter. In the body of the function, it changes the fill color to red and then uses the parameters to draw a circle.

To call this function, we’d just use its name and give it parameters, exactly like we’ve been calling preexisting functions:
```java
drawRedCircle(100, 200, 50);
```

This allows us to treat a task that takes multiple steps (like changing the fill color to red and drawing a circle) as a single step. As we do more complicated tasks, this becomes very useful.

**Below a more extensive example with smileys.**
```java
void smiley(int x, int y, int s) {
  noFill();
  stroke(0);
  strokeWeight(s/40);
  ellipse(x, y, s, s) ; // head
  ellipse(x-s/5, y-s/5, s/5, s/5);
  ellipse(x+s/5, y-s/5, s/5, s/5);
  arc(x, y, s*0.65, s*0.65, 0, PI, OPEN);
}

void setup() {
  size(520, 400);
  background(255);
  for (int x = 20; x < width; x+=40) {
    for (int y = 20; y < height; y+=40) {
      smiley(x, y, 40);
    }
  }
  smiley(width/2, height/2, 200);
}
```
  
## <a name="arrays">22. Arrays</a>
[see also the tutorial Arrays by Casey Reas and Ben Fry](https://processing.org/tutorials/arrays/)

**An array is a list of variables** that share a common name. Arrays are useful because they make it possible to work with more variables without creating a new name for each. Each item in an array is called **an element**, and each has an **index value** to mark its position within the array, starting from 0. 

So if you have an Array called cities[] then you might have items in that array called Gent, Brugge, Brussel and Antwerpen. We could then easily refer to any one of these items in the array by referring to the Array index number. Here is what the code would look like:

```java
String [] cities;          // Declare
cities = new String[4];    // Create
cities[0] = "Gent";        // Assign
cities[1] = "Brugge";
cities[2] = "Brussel";
cities[3] = "Antwerpen";

println(cities[2]);
```
The [] square bracket symbol denote that we are using an Array.    

You define an array first by **the data type** of object that will be held in it (in this case a String), followed by the **[] square brackets**, then **the name** of the Array.    
Then we need to create it. We repeat the given name, have **an equal sign** followed by **the word 'new'**. The new part tells Processing to free up some memory for the Array. We then denote the same Data Type that we were using in the beginning of the line of code. Finally, in the [] square brackets we put **how many items we want the array to hold**.

Thus: 
```Java
DataType [] ArrayName      
ArrayName = new DataType[length];
```
or shortened:
```Java
DataType [] ArrayName = new DataType[length];
```
You can also declare, create & assign an array in one go. 

```java
size(400,150);
strokeWeight(15);

int[] x = { 
  50, 61, 83, 69, 71, 50, 29, 31, 17, 39, 82, 93, 35, 96, 54
};

fill(0);
// Read one array element each time through the for loop
for (int i = 0; i < x.length; i++) {
  line(i*(width/x.length), height, i*(width/x.length), height-x[i]);
}
```

The `x.length` statement above queries the number of elements in an array. This .length is called dot operator.
```java
int[] data = { 19, 40, 75, 76, 90 };
println(data.length); // Prints "5" to the console
```

#### :hammer_and_wrench: An example: A Network

```java
// A Network
int points = 20;
int[] x = new int[points];
int[] y = new int[points];

void setup() {
  size(800, 500);
  for (int i = 0; i<points; i++) {
    x[i] = int(random(width));
    y[i] = int(random(height));
  }
  strokeWeight(1);
  fill(0);
  textSize(16);
}

void draw() {
  background(255);
  strokeWeight(0.5);
  for (int i =0; i<points; i++) {
    for (int j = i+1; j<points; j++) {
      noStroke();
      ellipse(x[i], y[i], 10, 10);
      text(i,x[i]+5, y[i]+10);
      stroke(0);
      line(x[i], y[i], x[j], y[j]);
      
    }
  }
}

```
![](images/processing/network.png)
_a Network_




## buttons & sliders
https://creative-coding.decontextualize.com/browser-controls/
