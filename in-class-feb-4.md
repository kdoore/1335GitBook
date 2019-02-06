###Class Code - Feb 4
In class code for Monday Feb 4, 
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
  PShape s2  = createShape( RECT, 0, 0, len2, len2);
  float hue = hue( c1);
  float sat = saturation(c1);
  float bright = brightness( c1);
  color c2 = color( hue, sat, bright * 0.8 );//reduce brightness
  s2.setFill( c2);  //set fill after creating the shape


  PShape s3 = createShape( GROUP); //create a group type PShape

  s3.addChild( s); //add both children to the group
  s3.addChild( s2);
  return s3; //return the group PShape
}


```

