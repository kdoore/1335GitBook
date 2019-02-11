#Class Code Feb 11
Simple Recursive Patterns
Size gradient using map()
Shape determined by region:  left or right of the balance point
Color Gradients using lerpColor() and map( ) functions

```java

float lenMax;
float lenMin;
PShape s;

void setup() {
  size( 600, 600);
  //fullScreen();
  colorMode(HSB, 360, 100, 100, 100);
  lenMax = width/4;  //set lenMax based on canvas width
  lenMin = width/30; //
  background(0);
}

void draw() {
  if ( mousePressed  &&  frameCount % 10 == 0 ) { //pattern only drawn once per ten frames
    //draw our pattern
    float balancePoint = width/2;  //default value is width midpoint 
    //colors to represent Negative Emotion Range
    //Negative primary color gradient Max to min
    color  c1NegativeMax = color(260, 100, 90 ); //dark purple
    color  c1NegativeMin = color(290, 70, 50); //dark magenta

    //colors to represent Positive Emotion Range
    //primary color gradient positive Max to min
    color  c3PositiveMax = color(200, 100, 100); //blue
    color  c3PositiveMin = color( 70, 100, 100  ); //bright lime
  
    //Define Parameters used for pattern size, stacking, rotation-count, colors across 2 regions

    int recursionCount;  //how many recursive layers per petal?

    //main input parameters for Recursive Functions
    float len; //determines size of PShape
    color cMain;
    color cVariant;
    float gradientFraction;

    // fraction = map( mouseX, 0, width, 0.0, 1.0);  //
    // cMain = lerpColor( c3Negative, c1Negative, fraction); //Main lime to purple transition
    float rand = random( 0.0, 1.0); //generate a random number each frame

    //Determine all parameter values before calling Pattern function
    //Left SIDE OF THE BALANCE POINT - POSITIVE COLORS
    //Determine Paramters for the left side: len, cMain, cVariant, 
    if ( mouseX < balancePoint ) {  ///left side  - positive  - flat design
      recursionCount = int(map( mouseX, 0, balancePoint, 3, 6)); //increasing

      len  = map( mouseX, 0, balancePoint, lenMax, lenMin);
      gradientFraction = map( len, lenMin, lenMax, 0.0, 1.0);  //small to large

      cMain = lerpColor( c3PositiveMin, c3PositiveMax, gradientFraction); //min to max
      cVariant = c3PositiveMin; //pop of color
     
    } else {   //Negative emotion - deep and complex
      recursionCount = int(map( mouseX, balancePoint, width, 5, 12)); //how much depth?

      len = map( mouseX, balancePoint, width, lenMin, lenMax);
      gradientFraction = map( len, lenMin, lenMax, 0.0, 1.0);  //small to large

      cMain = lerpColor( c1NegativeMin, c1NegativeMax, gradientFraction); //min to max
      cVariant = color(150); //
    }

    translate( mouseX, mouseY);
    float randAngle = random( -90, 45);
    rotate( radians(randAngle));
    //draw design
    if ( mouseX < balancePoint) {
      recursivePattern1( len, recursionCount, cMain, cVariant);  //create a single motif
    } else {
      recursivePattern2( len, recursionCount, cMain, cVariant);
    }
    resetMatrix(); //undo all transforms - (last translation(mouseX, mouseY))
  }  //end if mousePressed
} //end draw


/*RECURSIVE PATTERN1- Ellipse
color gradient within a shapeMotif is defined
as fractional value based on len compared to lenMin, lenMax */
void recursivePattern1( float len, int count, color c1, color c2) {
  if ( count < 1) {
    return;  //termination condition
  }
  float brightFraction = map( len, lenMin, lenMax, 0.6, 1.0); //as len increases, brightfraction increases
  float alphaFraction = map( len, lenMin, lenMax, 0.1, 1.0); //as len increases, alphaFraction increases

  color calcColor = color( hue(c1), saturation(c1), brightness(c1) *brightFraction, 100 * alphaFraction);
  float rand = random(0.0, 1.0); //random chance
  if ( rand < 0.3) {  //small chance of Pop c2
    calcColor = color( hue(c2), saturation(c2), brightness(c2) * brightFraction, 80 * alphaFraction);
  }

  //Create and draw shape
  PShape s=shapeEllipse( len, calcColor );  //draw the shape using current value of len
  shape( s, 0, 0);

  //recursive function call
  recursivePattern1( len * 0.8, count - 1, c1, c2); ///Recursive Call
}

/*RECURSIVE PATTERN2- Rectangles
color gradient within a shapeMotif is defined
as fractional value based on len compared to lenMin, lenMax */

void recursivePattern2( float len, int count, color c1, color c2) {
  if ( count < 1) {
    return;  //termination condition
  }
  PShape s;
  float brightFraction = map( len, lenMin, lenMax, 1.0, .4); //small len, max brightness
  float alphaFraction = map( len, lenMin, lenMax, .4, 1.0); //small len, small alpha

  color calcColor = color( hue(c1), saturation(c1), brightness( c1) * brightFraction, 100 * alphaFraction);

  float rand = random(0.0, 1.0); //with randome chance
  if ( rand < 0.2) {  //small chance of Pop c2
    calcColor = color( hue(c2), saturation(c2), brightness(c2)* brightFraction, 100 * alphaFraction);
  }
 //create and draw first shape
  s =shapeRect( len, calcColor );  //draw the shape using current value of len
  shape( s, 0, 0);

  //recursive call
  recursivePattern2( len * 0.8, count - 1, c1, c2); 
  
  //create and draw second shape ( with reversed layer ordering)
  s= shapeRect( -len *.4, calcColor);
  shape(s, 0, 0);
}


PShape shapeEllipse(float len, color c) {
  PShape s = createShape( ELLIPSE, 0,0, len *.8, len);
  s.setFill(c);
  return s;
}

PShape shapeRect(float len, color c) {
  PShape s = createShape( RECT, 0, 0, len, len * .8);
  s.setFill(c);
  return s;
}

```

