# Intersecting Agents

As we begin our look at dynamic patterns, we can start with a simple ball class that is covered in Chapter 10 of Shiffman's book.  He creates a simple Ball class that has position and speed instance variables.  He adds methods to display(), move(), and intersect(Ball b). We can create lists or arrays of these ball objects, and then we can animate these Ball objects by calling move() and display() methods within the processing draw loop.

![](Screenshot 2016-11-10 19.21.07.png)

Below is our custom code for a Ball class

```java
class Ball{
  float x, y, r, speedX, speedY;
  color curColor, highlightColor, basicColor;
  
  //constructor
  Ball(float _x,float _y){
    x= _x;
    y = _y;
    r = random(5,25);  ///radius is for test intersection
    speedX  = random(1,3);
    speedY = random(1,3);
    highlightColor = color(#AEFF1A);
    basicColor = color(#7C1AFF);
    curColor = basicColor;
  }
  
  void display(){
    fill(curColor);
    ellipse(x,y, 2*r,2*r); 
    curColor= basicColor;
  }
  
  void highlight(){
    curColor = highlightColor;
  }
  
  void reverseX(){
    speedX *= -1;
  }
  
  void move(){
    if( x >width || x < 0){
      speedX *= -1;
    }
    if( y > height || y < 0){
      speedY *= -1;
    }
    
    x += speedX;
    y += speedY;
  }
  
  
  boolean intersect( Ball b){
    boolean isIntersect = false;
    float d = dist(this.x, this.y, b.x, b.y);
    if(d < this.r + b.r){
      isIntersect= true;
    }
   return isIntersect;
  }
  
  
} // end Ball class

```

#Main Tab - Array of Ball objects

In the main tab code, shown below, we create an array of Ball objects.  In setup(), we initialize all Ball objects so they have a random position on the canvas.

Then, we want to check for intersection of ball objects.  To do that, we loop through all Ball objects.  For each Ball object, we check all other ball objects using an inner-loop, with j as the index variable, and we check to see if there's intersection.  If there is intersection, then we color both Ball objects with the highlight color, and we also reverse the  Xspeed direction for both of the balls.  We can start to see the Balls acting as agents, with shared interactive behaviors, some Ball objects appear to dance together for a few moments.


```java
Ball[] balls; //declare array of Ball objects
int numBalls;

void setup(){
  size(700,700);
  numBalls = 50;
  balls = new Ball[numBalls];// initialize array
  for (int i=0; i<numBalls; i++){
    float x= random(0,width);
    float y= random(0,height);
    balls[i] = new Ball(x,y);
  }
}


void draw(){
  background(0);
  //for every ball, check all other balls to see if there's an intersection
  //if there's an intersection, change color of both balls and
  //reverse X direction of both balls using Ball class methods
  for (int i=0; i<numBalls; i++){
    for( int j = 0 ; j < numBalls; j++){
      if( i != j){
        if(balls[i].intersect( balls[j])){
               balls[i].highlight();
               balls[i].reverseX();
               balls[j].highlight();
               balls[j].reverseX();
        }
      }
     }
     ///for all Ball objects - move and display the objects
    balls[i].move();
    balls[i].display();
    } 
}

```