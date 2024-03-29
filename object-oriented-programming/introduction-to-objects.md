# Introduction to Objects

## What's an object?  Who cares?

> **An object is just like you, a thing that has properties and can do stuff.**
>
> So, how does this relate to programming? **The properties of an object are variables, and the things an object can do are functions**. Object-oriented programming is the marriage of all of the programming fundamentals: data and functionality.\
> \
> &#x20; [**Processing Website**](https://processing.org/tutorials/objects/) **- OOP Tutorial - Daniel Shiffman**

\
\
To begin our look at Object oriented programming, we'll look at the simple task of animating a ball moving across the Processing canvas.

First, we'll look at the code in the Ball Class Definition, then we'll look at the main tab code to see how to create an instance of a Ball Class object.

Below is a UML (Unified Modeling Language) Class diagram which gives an overview of the important information about the Ball class. In the top section is the class name, the second section shows the instance variables or properties of the class. The bottom section shows the class methods, which are functions that belong to the class. [UML Class Diagram Specification](https://www.uml-diagrams.org/class-diagrams-overview.html)

![](../.gitbook/assets/screenshot-2016-09-16-08.30.08.png)

## Objects:  Data and Functionality (Behaviors)

A object can be considered as a type of thing that we could classify based on its' features or attributes, where these classification details can be considered as the object's data.  Because humans organize our reality using the concept of objects, it is intuitive to design programs using an object metaphor to organize and structure our code.\
The object-oriented paradigm considers that objects have functionality or behaviors.  In order to create objects in a program, we must write code to create a **class definition** that specifies all the information required to provide the data and functionality for the object instances created when the program is executing. &#x20;

### Class Definition

The \


[Link to Zip file of Example Code Below](https://utdallas.box.com/shared/static/j0guoj7qop0bxfblniocj4spixqnguuw.zip)

```java
//Definition for Ball Class

class Ball{
  //instance variables or properties
  float x; 
  float y;
  float size;

   //additional variables (these ones are not shown in UML Class Diagram)
  float speedX;
  float speedY;
  color ballColor;

  //////Class Constructors - to initialize instance variables
  /////Overloaded versions - each with a unique parameter list
  Ball(){  //default constructor takes no input parameters
    this( 5, 5, 50); //calls the Ball constructor Ball(5,5,50)
  }

  Ball(float _x, float y, float size ){
    x = _x;  //initialize instance variable: x
    this.y  = y;  //initialize instance variable: y
    this.size = size;
    speedX = 5;  //the same for every object
    speedY = 10;  //the same for every object
    ballColor = color( 100); //default ball color is gray
  }

  Ball(float _x, float y, float size, float speedX, float speedY, color ballColor ){
    x = _x;  //initialize instance variable: x
    this.y  = y;
    this.size = size;
    this.speedX = speedX;  //the same for every object
    this.speedY = speedY;  //the same for every object
    this.ballColor = ballColor;
  }

  ////////////Methods or functions

  //displays the ball
  void display(){
    fill( ballColor);
    ellipse( x, y, size, size); //diameter
  } //end display method

  //determines new position for ball each time this is executed
  void move(){
    if( x > width || x < 0){
      speedX *= -1;
    }
     if( y > height || y < 0){
      speedY *= -1;
    }
    x += speedX;
    y += speedY;
  } // end move method

} //end of class Ball

////Main Tab Code:

Ball ball1;   //ball1 = null
//declare a variable that can point to a ball object's data in heap memory

Ball[] balls; //declare the array of Ball objects

void setup() {
  size( 600, 600);
  colorMode(HSB, 360,100,100);
  ///create 1 Ball object instance
  ball1 = new Ball(20, 20, 30, 15, 5, color(255, 0, 0)); //new is the keyword used to create an object instance

balls = new Ball[100]; //initialize the array

  for ( int i=0; i< balls.length; i++) {
    float x = random(0, width);
    float y = random(0, height);
    float hue = random(0, 360);
    balls[i] = new Ball(x, y, 20, 5, 10, color( hue, 100, 100)); //called the constructor - we have an object instance
  } //end of for
}//end of setup


void draw() {
  background(255);

  //have each ball execute it's move method
  ball1.move();

  //have each ball display itself
  ball1.display();

  //use for-loop to move and display all balls
  for ( int i=0; i< balls.length; i++) {
    balls[i].move();
    balls[i].display();
  } //end for


} //end draw
```
