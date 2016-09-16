#Introduction To Objects

To begin our look at Object oriented programming, we'll look at the simple task of animating a ball moving across the Processing canvas.

First, we'll look at the code in the Ball Class Definition, then we'll look at the main tab code to see how to create an instance of a Ball Class object.


```java
class Ball {

  int x, y, size; ///instance variables
  color ballColor;

  ////Constructor

  Ball() {  //default constructor
    this( 20, 50, 30);  //default instance variables
  }

  Ball(int _x, int _y, int _size) {
    x=_x;
    y= _y;
    size = _size;
    ballColor = color(255, 0, 0);
  }

  ///Methods
  void display() {
    fill(ballColor);
    ellipse(x, y, size, size);
  }
  
  void move(){
    x += 3;
    println(" x " + x);
  }

}////end of Ball class

////Main Tab Code:

Ball ball1; ///declared Ball object reference 
int myVal;   //declare int variable

void setup(){
  size(400,400);
  myVal = 5;   //initializing our integer
  ball1 = new Ball();  //initializing our Ball object 
}

void draw(){
  background(255);
  ball1.move();
  ball1.display();   //dot notation to call a method
  }

```

