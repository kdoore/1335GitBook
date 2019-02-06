###Creating PShapes and using map( )
**Overview: In-class code for Monday Feb 4** 
On Feb 4, We wrote a program to explore using PShapes and the map( ) function.  

We wrote function with the following signature:
 
 ` PShape customShape1(float len , color c1 )` 
 
 This function creates and returns a new PShape object:
   
   - input parameter: len - to define the size of the PShape.
   - input parameter: c1 - defines the fill color for the shape
 
In the Processing draw( ) function, if mousePressed is true, then we:
   - move the origin to the mouse location
   - use map( ) to do a calculation to initialize the value of float len, such that:
     - as mouseX gets larger, len gets larger 
     - if mouseX is 0, then len is lenMin
     - if mouseX is width, then len is lenMax
   - call customShape1(  len, c1 ); with calculated value for len 
   - resetMatrix( ) , to move the origin back to default position
    
 We also played with the idea of creating complex PShapes using the statement; `PShape s3 = createShape( GROUP );`
In this case, we created 2 PShapes, where the 2nd shape is a smaller, darkened version of the first shape, where we simply multiplied: len * 0.8, bright * 0.8, before using to create the 2nd shape.

###Class Code - Feb 4

```java

float lenMax, lenMin;

void setup() {
  size( 600, 600);
  colorMode(HSB, 360, 100, 100, 100);
  rectMode(CENTER); //sets x,y for rectangles as the center of the rectangle
  background( 0);
  lenMin = 20;
  lenMax = 200;
}

void draw() {
  if ( mousePressed) {
    translate( mouseX, mouseY);
    color c1 = color(270, 100, 80);
    float len = map(  mouseX, 0, width, lenMin, lenMax); //as mouseX gets bigger, len gets bigger
    PShape myShape = customShape1( len, c1); //get a shape based in input values: float len, color c1
    shape( myShape, 0, 0); //display a shape
    resetMatrix();
  }
}


//creates and returns one PShape object using input parameters
PShape customShape1(  float len, color c1) {
  PShape s = createShape(RECT, 0, 0, len, len);
  s.setFill( c1 );
 return s; //return the group PShape
}

//more complicated version creates a GROUP-type PShape

//color is darkened prior
//creates and returns one PShape object using input parameters
PShape customShape2(  float len, color c1) {
  PShape s = createShape(RECT, 0, 0, len, len);
  s.setFill( c1 ); //set fill after creating the shape
  
  float len2 = len * 0.8;
  float hue = hue( c1);
  float sat = saturation(c1);
  float bright = brightness( c1);
  color c2 = color( hue, sat, bright * 0.8 );//reduce brightness
  //create smaller, darker Rectangle
  PShape s2  = createShape( RECT, 0, 0, len2, len2);
  s2.setFill( c2);  //set fill after creating the shape


  PShape s3 = createShape( GROUP); //create a group type PShape

  s3.addChild( s); //add both children to the group
  s3.addChild( s2);
  return s3; //return the group PShape
}


```

# Loops, Introduction to Recursion:  
### Repeat to create Nested Shapes

**Overview: Class Code - Feb 6, 2019**

To introduce the idea of Recursion, we first went to look at repeating a single shape, multiple times, each time the mouse is pressed.  Visually, this is more interesting if we have an Asymmetric form, so we're not going to use rectMode(CENTER) in this example. 

In order for a repeat to be visibly noticible, we'd like to have 1 shape drawn at the same position, but we'd like to have each successive shape-motif be slightly smaller and darker than the one drawn previously.  So, as with the code on Feb 4, we want to change len, and the brightness of c1 each time we create and render a shape.


#Class Code Feb 6
```java
float lenMax, lenMin;

void setup() {
  size( 1000, 1000);
  colorMode(HSB, 360, 100, 100, 100);
  //rectMode(CENTER); //remove this code, we want an asymetric form to create interesting patterns
  background( 0);
  lenMin = 20;
  lenMax = 200;
}

void draw() {
  if ( mousePressed && frameCount % 5 == 0 ) { //no remainder happens every 10 frames
    translate( mouseX, mouseY);
    color c1 = color(270, 100, 100);
    float len = map(  mouseX, 0, width, lenMin, lenMax); //as mouseX gets bigger, len gets bigger
    int numRepeats = 5;
    repeatPattern( len, c1, numRepeats);
    resetMatrix();
  }
}

//create a recursivePattern: 
//recursive function must have a recursive call statement ( where it calls itself)

void recursivePattern(float len, color c1, int count  ) {
  //test for termination - must happen before the recursive call
  if ( count < 0) { //terminate if this conditional test is true
    return;  ///don't execute any more code in this function
  }
  ///where do we do our task? before the recursive call?

  count--; //make sure our termination variable will meet the termination stop condition
  recursivePattern( len, c1, count ); //calls itself - recursive call

  ///where do we do our task? after the recursive call?
}


//repeat pattern using a for loop
void repeatPattern( float len, color c1, int count  ) {
  for ( int i = 0; i< count; i++) {  //make sure this stops
    float fraction = map( i, 0, count-1, 1.0, 0.2); //as i goes from small to big, len should go from big to small
    float hue = hue( c1);
    float sat = saturation (c1);
    float bright = brightness( c1);
    bright *= fraction; //reduce bright each time 
    color c2 = color( hue, sat, bright);
    PShape myShape = customShape2( len * fraction, c2); //get a shape based in input values: float len, color c1
    shape( myShape, 0, 0); //display a shape
  }
}


PShape customShape2(  float len, color c1) {
  PShape s = createShape(RECT, 0, 0, len, len);
  s.setFill( c1 );
  return s;
}


```


