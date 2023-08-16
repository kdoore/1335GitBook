# Example Code

This is the code covered in class Starting on Jan 30, 2019

```java
//Spring 2019 - Jan30 Class Code
void setup(){
  size( 600, 600);
  colorMode(HSB, 360, 100, 100); ///
}

void draw(){
  translate( width/2, height/2);
  float angleSize = map( mouseX, 0, width, 1, 90);
  drawColorWheel( 600, angleSize); //
  resetMatrix();
}

///Custom functions
void drawColorWheel( float size, float angleSize   ){

  float startDegree = 0;
  float endDegree = startDegree + angleSize;
  int numSlices = int(360.0/ angleSize); //truncating
  float sat = 100;
  float bright = 100;


  for( int i= 0; i< numSlices; i++){ 
    float hue = startDegree; //changes each time that startDegree
    fill(hue, sat, bright );
    arc(0,0, size, size, radians(startDegree), radians(endDegree));
    startDegree += angleSize;
    endDegree += angleSize; 
  }
}
```
