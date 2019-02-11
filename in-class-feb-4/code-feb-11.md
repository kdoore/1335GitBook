#Class Code Feb 11
Simple Recursive Patterns
Size gradient using map()
Shape determined by region:  left or right of the balance point
Color Gradients using lerpColor() and map( ) functions

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
    color c1 = color(270, 100, 100);  //purple - negative color
    float len; //this will vary depending on region and mouse position
    int numRepeats = 10;

    if ( mouseX < balancePoint) { //in the left region of the canvas - Negative
      len = map(  mouseX, 0, balancePoint, lenMax, lenMin); //as mouseX gets bigger, len gets smaller
      translate( mouseX, mouseY);
      rotate(radians( random( 0, 180)));
      recursivePattern1( len, c1, numRepeats); //rectangle is for netagive
      resetMatrix();
    } else { //in the right region - Positive
      len = map(  mouseX, balancePoint, width, lenMin, lenMax); //as mouseX gets bigger, len gets bigger
      translate( mouseX, mouseY);
      rotate(radians( random( 0, 180)));
      recursivePattern2( len, c2, numRepeats);
      resetMatrix();
  }
  }
}

//create a recursivePattern: 
//recursive function must have a recursive call statement ( where it calls itself)

void recursivePattern1(float len, color c1, int count  ) {
  //test for termination - must happen before the recursive call
  if ( count < 0) { //terminate if this conditional test is true
    return;  ///don't execute any more code in this function
  }
  ///where do we do our task? before the recursive call?
  float fractionBright = map(len, lenMin, lenMax, 1.0, 0.1);
  float hue = hue( c1) ;
  float sat = saturation (c1);
  float bright = brightness( c1);
  bright *= fractionBright; //reduce bright each time 
  color c2 = color( hue, sat, bright);
  PShape myShape = customShape1( len, c2); //get a shape based in input values: float len, color c1
  shape( myShape, 0, 0); //display a shape
  //make sure our termination variable will meet the termination stop condition
  recursivePattern1( len * 0.8, c1, count-1 ); //calls itself - recursive call

  myShape = customShape1( -len *0.4, c2); //get a shape based in input values: float len, color c1
  shape( myShape, 0, 0); //display a shape

  ///where do we do our task? after the recursive call?
}



void recursivePattern2(float len, color c1, int count  ) {
  //test for termination - must happen before the recursive call
  if ( count < 0) { //terminate if this conditional test is true
    return;  ///don't execute any more code in this function
  }
  ///where do we do our task? before the recursive call?
  float fractionBright = map(len, lenMin, lenMax, 1.0, 0.1);
  float hue = hue( c1) ;
  float sat = saturation (c1);
  float bright = brightness( c1);
  bright *= fractionBright; //reduce bright each time 
  color c2 = color( hue, sat, bright);
  
  PShape myShape = customShape2( len, c2); //get a shape based in input values: float len, color c1
  shape( myShape, 0, 0); //display a shape
  //make sure our termination variable will meet the termination stop condition
  recursivePattern2( len * 0.8, c1, count-1 ); //calls itself - recursive call

  myShape = customShape2( -len *0.4, c2); //get a shape based in input values: float len, color c1
  shape( myShape, 0, 0); //display a shape

  ///where do we do our task? after the recursive call?
}



PShape customShape2(  float len, color c1) {
  PShape s = createShape(ELLIPSE, len*.2, len*.3, len *.8, len);
  s.setFill( c1 );
  return s;
}

PShape customShape1(  float len, color c1) {
  PShape s = createShape(RECT, 0, 0, len *.8, len);
  s.setFill( c1 );
  return s;
}


```

