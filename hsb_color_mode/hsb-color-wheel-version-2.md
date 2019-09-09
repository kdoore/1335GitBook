# HSB ColorWheel CS1335.002_F19

```java

float angleSize=1;
float sat, bright;

void setup() {
  size( 600, 600);
  colorMode(HSB, 360, 100, 100);
  noStroke();
  sat=100;
  bright=100;
  int r = (int)random( 2, 5 );

}

void draw() {
  background(0);
  translate( width/2, height/2);
  angleSize = map( mouseX, 0, width, 1, 90);
  //angleSize=10;
  if ( mousePressed) {
    satGradientColorWheel(width, angleSize);
  } else {
    brightGradientColorWheel(width, angleSize);
  }
  resetMatrix();
}

void brightGradientColorWheel( float size, float angleSize ) {
  sat=100;
  for ( int i=100; i>0; i -=5) {
    bright = i;
    drawColorWheel((size * i)/100.0, angleSize);
  }
}


void satGradientColorWheel(float size, float angleSize) {
  bright=100;
  for ( int i=100; i>0; i -=5) {
    sat = i;
    drawColorWheel((size * i)/100.0, angleSize);
  }
}


void drawColorWheel( float size, float angleSize ) {
  //initialize all of the local variables
  float hue = 0;
  float startDegree = 0;
  float endDegree =  angleSize;
  int numSlices = int(360/ angleSize); //cast to integer
  ///repeat
  for ( int i=0; i< numSlices; i++) {
    fill( hue, sat, bright);
    arc( 0, 0, size, size, radians(startDegree), radians(endDegree));
    ///update all values for each next arc
    startDegree += angleSize;
    endDegree += angleSize;
    hue = startDegree;
  }
}

```



