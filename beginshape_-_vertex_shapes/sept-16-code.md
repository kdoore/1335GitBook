###Example Code

```java

float maxLen = 100;

void setup( ) {
  size( 600, 600);
  colorMode(HSB, 360, 100, 100, 100);//HSBA
  background(360);
}

void draw( ) {
  color purple = color( 270, 100, 100); 

  if ( mousePressed) {
    translate( mouseX, mouseY); //move origin to mouse postion
    recursivePattern1( maxLen, 5, purple);
    resetMatrix(); //move origin back to upper left
  }
}
void recursivePattern1(  float len, int level, color c1    ) {
  if ( level<1) { //termination condition
    return;//stops the function from executing
  }
  //TASK for the recursive function
  float fraction = map( len, 0, maxLen, 0.4, 1.0);
  color curColor = color( hue( c1), saturation(c1), brightness(c1) * fraction );
  PShape s1 = createShape1( len, curColor );

  shape( s1, 0, 0);

  recursivePattern1( len * 0.8, level-1, curColor);
 
}


PShape createShape1(  float len, color c1) {
  //fill( c1); //for some PShapes, use fill before creating the shape
  PShape s = createShape(RECT, 0, 0, len, len) ;
  s.setFill( c1);//for some PShapes, use setFill( ) after creating the shape

  return s;
}

```

