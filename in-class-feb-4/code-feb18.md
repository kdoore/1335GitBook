#Class Code - Feb 18

```java

float lenMax, lenMin;

void setup() {
  size( 1000, 1000);
  colorMode(HSB, 360, 100, 100, 100);
  //rectMode(CENTER); //remove this code, we want an asymetric form to create interesting patterns
  background( 0);
  lenMin = 5;
  lenMax = 200;
}

void draw() {
  if ( mousePressed && frameCount % 5 == 0 ) { //no remainder happens every 10 frames
    float balancePoint = width/2;
    
    color c1Max = color(270, 100, 100); //purple - negative color
    color c1Min = color( 310, 50, 50);//dark magenta
    color c1Variant = color( 243, 100, 100 ); //pop of color - blue
    
    color c2Max = color( 31, 100, 100 ); //orange - positive color
    color c2Min = color ( 92, 100, 100); //green bright - positive
    color c2Variant = color(20, 100 ,100);//dk orange, pop of color
    
    float len; //this will vary depending on region and mouse position
    int numRepeats = 10;
    float gradFraction;
    translate( mouseX, mouseY);
    color cMain;
    float rand = random( 0.0, 1.0);
    ////NEGATIVE REGION
    if ( mouseX < balancePoint) { //in the left region of the canvas - Negative
      len = map( mouseX, 0, balancePoint, lenMax, lenMin); //as mouseX gets bigger, len gets smaller
      gradFraction = map( mouseX, 0, balancePoint, 0.0,1.0 );
      cMain = lerpColor( c1Max, c1Min, gradFraction);  //gradient of color, calculate color for current mouseX position
      if( rand < 0.3){
        cMain = c1Variant;
      }
      recursiveRectPattern( len, cMain, numRepeats); //rectangle is for netagive

    } 
    //////POSITIVE REGION
    else { //in the right region - Positive
      len = map( mouseX, balancePoint, width, lenMin, lenMax); //as mouseX gets bigger, len gets bigger

      cMain = c2Max; //calculate using lerpColor
      recursiveEllipsePattern( len, cMain, numRepeats);

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
  color c2 = color( hue(c1), saturation(c1), bright);
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
  float fractionBright = map(len, lenMin, lenMax,0.4, 1.0);
  float bright = brightness( c1) * fractionBright;//reduce bright each time
  float hue = hue(c1) + random( -10, + 10); //small random variation in hue
  color c2 = color( hue, saturation(c1), bright);

 //Recursive task - create and display shape
   PShape myShape = customEllipse( len, c2); //get a shape based in input values: float len, color c1
  shape( myShape, 0, 0); //display a shape
  //make sure our termination variable will meet the termination stop condition

  //RECURSIVE FUNCTION IS CALLED
  recursiveEllipsePattern( len * 0.8, c1, count-1 ); //calls itself - recursive call

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
//Example custom PShape using vertex( ) points
PShape customShape3( float len, color c1){
  PShape s = createShape();
  s.beginShape();
  s.fill( c1);  //syntax for fill with vertex shapes
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

