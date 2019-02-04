###Class Code - Feb 4, Feb 6
In class code for Monday Feb 4, Wed Feb 6, 2019

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
  PShape s2  = createShape( RECT, 0, 0, len * 0.8, len * 0.8);
  s2.setFill( color(hue( c1 ), saturation ( c1), int(brightness( c1 ) * 0.8)));

  PShape s3 = createShape( GROUP); //create a group type PShape

  s3.addChild( s); //add both children to the group
  s3.addChild( s2);
  return s3; //return the group PShape
}


```

