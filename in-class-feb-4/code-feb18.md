#Class Code - Feb 18

```java

void setup() {
  size( 1000, 1000);
  colorMode(HSB, 360, 100, 100, 100);
  background( 0);
  lenMin = 20;
  lenMax = 200;
}

void draw() {
  if ( mousePressed && frameCount % 5 == 0 ) { //no remainder happens every 10 frames
    float balancePoint = width/2;
    color c2Max = color( 31, 100, 100 ); //orange - positive color
    color c2Min = color(100,  100, 100);  //green
    color c1Max = color(270, 100, 100); //purple - negative color
    color c1Min = color( 170, 50, 50); //aqua - dark
    color c1Pop = color(200, 100, 100);
    color c2Pop = color( 70, 100, 100);
    
    float len; //this will vary depending on region and mouse position
    int numRepeats = 10;
    color cMain;
    float gradFraction;
    float rand = random( 0.0, 1.0);
    
    translate( mouseX, mouseY);

    if ( mouseX < balancePoint) { //in the left region of the canvas - Negative
      len = map( mouseX, 0, balancePoint, lenMax, lenMin); //as mouseX gets bigger, len gets smaller
      gradFraction = map( mouseX, 0, balancePoint, 0.0, 1.0);
      cMain = lerpColor( c1Max, c1Min, gradFraction);
      
      if(rand < .3){ //pop of color
        cMain = c1Pop;
      }
      
     
      recursiveRectPattern( len, cMain, numRepeats); //rectangle is for netagive

    } 
    else { //in the right region - Positive
      len = map( mouseX, balancePoint, width, lenMin, lenMax); //as mouseX gets bigger, len gets bigger
      gradFraction = map( mouseX, balancePoint, width, 0.0, 1.0);
      cMain = lerpColor( c2Min, c2Max, gradFraction);
       if(rand < .3){ //pop of color
        cMain = c2Pop;
      }
    
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
  float bright = brightness( c1) * fractionBright; //max bright when lenMin
  color c2 = color( hue(c1), saturation(c1), bright);
  PShape myShape = customRect( len, c2); //get a shape based in input values: float len, color c1
  shape( myShape, 0, 0); //display a shape
  //make sure our termination variable will meet the termination stop condition
  //RECURSIVE FUNCTION CALL
  recursiveRectPattern( len * 0.8, c1, count-1 ); //calls itself - recursive call
  //this will be reversed stacked pattern since it's after the recursive call
  myShape = customRect( -len *0.4, c2); //get a shape based in input values: float len, color c1
  shape( myShape, 0, 0); //display a shape

} //end recursiveRectPattern



void recursiveEllipsePattern(float len, color c1, int count ) {
  //test for termination - must happen before the recursive call
  if ( count < 0) { //terminate if this conditional test is true
    return; ///don't execute any more code in this function
  }
  //Set variables for the recursive task
  float fractionBright = map(len, lenMin, lenMax, .30, 1.0);
  float hue = (hue(c1)+ random( -5, 10)); //add small random hue variation
  float bright = brightness( c1) * fractionBright;//max bright, with lenMax
  color c2 = color(hue , saturation(c1), bright);

 //Recursive task - create and display shape
   PShape myShape = customEllipse( len, c2); //get a shape based in input values: float len, color c1
   shape( myShape, 0, 0); //display a shape
  //make sure our termination variable will meet the termination stop condition

  //RECURSIVE FUNCTION IS CALLED
  recursiveEllipsePattern( len * 0.8, c1, count-1 ); //calls itself - recursive call
  ///we could add another recursive call here to have reversed pattern
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

```

