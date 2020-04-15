# Code  Wed Apr 1

#### Main Tab Code

```text
Ball ball1; //declare the variable

//initialization
void setup(){
  size( 400, 400);
  colorMode(HSB, 360, 100, 100);
  //Ball( float x, float y, float size  ){
  ball1 = new Ball( 10, 10, 50, color(0)); //create the object instance
  ball1.speedX= 5; //to 
 }
 
 
void draw(){
  background(360);
  ball1.move();
  ball1.display();
}
```

### Ball Class Tab Code

```text
class Ball{
  //Properties, attributes, instance variables
  float x, y;  //location
  float size; 
  
  float speedX, speedY;
  color ballColor;
  
  //Initialization ( like setup)
  //Constructors - pass in parameters to initialize attributes
  Ball( float x, float y, float size  ){
    this.x = x; //this keyword refers to the object instance 
                //currently executing the code
    this.y  = y;
    this.size = size;
    //Hard-coded values not passed in as parameters
    speedX = 3;
    speedY = 2;
    ballColor = color( 280, 100, 100); //HSB
  }
  //overloaded constructors
  Ball( float x, float y, float size, color ballColor  ){
    this.x = x; //this keyword refers to the object instance 
                //currently executing the code
    this.y  = y;
    this.size = size;
    this.ballColor = ballColor;
    //Hard-coded values not passed in as parameters
    speedX = 3;
    speedY = 2;
     }
  
  //Behaviors - Methods, functions
  void move(){
    x += speedX;
    y += speedY;
  }
  
  void display(){
    fill( ballColor);
    ellipse(x, y, size, size);
   }
  
}  //end class
```

