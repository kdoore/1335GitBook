# Example Code: PShape

The code below shows how to create a custom function that creates and returns a custom PShape object.  The PShape method: **shape\(PShape s, float x, float y \)**  is used in draw\( \) to render the shape by inputing the specified values for parameters:  x, y: 

```java

void setup( ) {
  size( 600, 600);
  colorMode(HSB, 360, 100, 100, 100);//HSBA
  background(360);  //white
}

void draw( ) {
  color purple = color( 270, 100, 100); 
  float len = 100;
  if ( mousePressed) {
    translate( mouseX, mouseY); //move origin to mouse postion
    PShape s = createMyShape1( len, purple); //create PShape
    shape( s, 0, 0 ); //display at translated origin
    resetMatrix(); //move origin back to upper left
  }
}


PShape createMyShape1(  float len, color c1) {
  //fill( c1); //for some PShapes, use fill before creating the shape
  PShape s = createShape(RECT, 0, 0, len, len) ;
  s.setFill( c1);//for some PShapes, use setFill( ) after creating the shape

  return s;
}
```

