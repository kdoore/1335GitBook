#Class Code Feb 11
Simple Recursive Patterns:

Recursion provides a repeat structure that we're using to create complex patterns from simple shapes. Each customShape function creates and returns a PShape using input parameter values: `float len, color c1.`

Each recursivePattern function creates a complex pattern by repeating the shape multiple times, where len, and brightness are modified before each repeat.

Size gradient using map()
Brightness Gradients using map( ) function
Shape determined by region:  left or right of the balance point


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
    float balancePoint = width/2;
    color c2 = color( 31, 100, 100 ); //orange - positive color
    color c1 = color(270, 100, 100); //purple - negative color
    float len; //this will vary depending on region and mouse position
    int numRepeats = 10;
    translate( mouseX, mouseY);

    if ( mouseX < balancePoint) { //in the left region of the canvas - Negative
      len = map( mouseX, 0, balancePoint, lenMax, lenMin); //as mouseX gets bigger, len gets smaller
      
      rotate(radians( random( 0, 180)));
      recursiveRectPattern( len, c1, numRepeats); //rectangle is for netagive
   
    } 
    else { //in the right region - Positive
      len = map( mouseX, balancePoint, width, lenMin, lenMax); //as mouseX gets bigger, len gets bigger
     
      rotate(radians( random( 0, 180)));
      recursiveEllipsePattern( len, c2, numRepeats);
      
    } //end else
    resetMatrix();

  } //end if mousePRessed
} //end draw

//create a recursivePattern:
//recursive function must have a recursive call statement ( where it calls itself)

void recursiveRectPattern(float len, color c1, int count ) {
  //test for termination - must happen before the recursive call
  if ( count < 0) { //terminate if this conditional test is true
    return; ///don't execute any more code in this function
  }
  ///where do we do our task? before the recursive call?
  float fractionBright = map(len, lenMin, lenMax, 1.0, 0.1);
  float bright = brightness( c1) * fractionBright; //reduce bright each time
  color c2 = color( hue(c1), sat(c1), bright);
  PShape myShape = customRect( len, c2); //get a shape based in input values: float len, color c1
  shape( myShape, 0, 0); //display a shape
  //make sure our termination variable will meet the termination stop condition
  //RECURSIVE FUNCTION CALL
  recursiveRectPattern( len * 0.8, c1, count-1 ); //calls itself - recursive call

  myShape = customRect( -len *0.4, c2); //get a shape based in input values: float len, color c1
  shape( myShape, 0, 0); //display a shape

} //end recursiveRectPattern



void recursiveEllipsePattern(float len, color c1, int count ) {
  //test for termination - must happen before the recursive call
  if ( count < 0) { //terminate if this conditional test is true
    return; ///don't execute any more code in this function
  }
  //Set variables for the recursive task
  float fractionBright = map(len, lenMin, lenMax, 1.0, 0.10);
  float bright = brightness( c1) * fractionBright;//reduce bright each time
  color c2 = color( hue(c1), sat(c1), bright);
 
 //Recursive task - create and display shape
   PShape myShape = customEllipse( len, c2); //get a shape based in input values: float len, color c1
  shape( myShape, 0, 0); //display a shape
  //make sure our termination variable will meet the termination stop condition
  
  //RECURSIVE FUNCTION IS CALLED
  recursiveEllipsePattern( len * 0.8, c1, count-1 ); //calls itself - recursive call

///where do we do our task? after the recursive call?
  myShape = customEllipse( -len *0.4, c2); //get a shape based in input values: float len, color c1
  shape( myShape, 0, 0); //display a shape 
} //end RecursiveEllipsePattern


PShape customEllipse( float len, color c1) {
  PShape s = createShape(ELLIPSE, len*.2, len*.3, len *.8, len);
  s.setFill( c1 );
  return s;
}

PShape customRect( float len, color c1) {
  PShape s = createShape(RECT, 0, 0, len *.8, len);
  s.setFill( c1 );
  return s;
}


//Vertex PShape
PShape customShape3( float len, color c1){
  PShape s = createShape();
  s.beginShape();
  s.fill( c1);
  s.vertex(0,0 ); //1
  s.vertex(.75 * len,.25 * len );//2
  s.vertex(len,.75 * len ); //3
  s.vertex(.25 * len, len ); //4
  s.vertex(0,.5 * len ); //5
  s.vertex(0,0 ); //6
 
  s.beginContour();
  s.vertex( .25 * len, .25 * len);
  s.vertex( .25 * len, .5 * len);
  s.vertex(.5 * len, .5 * len);
  s.vertex(.5 * len, .25 * len );
  s.endContour();
   s.endShape( CLOSE );
  return s;
}

```

