#HSB ColorWheel Version 2

The code in version 1 has several sections of repetitive code in the draw loop, where we're drawing smaller versions of the color-wheel.  How can we use functions and loops to simplify the logic?


```java

///Global variables
int hue, sat, bright;
void setup() {
  size( 600, 600);
  colorMode(HSB, 360, 100, 100);
  background(0);
  noStroke();
  sat = 100;
  bright = 100;
}

void draw( ) {
  background(0); //black background
  if (mousePressed) {
    brightGradientColorWheel(width);
  } else {
    satGradientColorWheel(width);
  }
}

//Function to draw 1 full colorWheel 
//parameter size - control size of colorWheel
//angleSize = 10 degrees
void drawColorWheel(float size ) {
  int angleSize = 10;
  int startDegree =0;
  int numSlices = 360/angleSize;
  noStroke();
  for (int i = 0; i< numSlices; i++) { //should this be <=?
    int endDegree = startDegree + angleSize;
    hue = startDegree + (angleSize/2);
    fill( hue, sat, bright);
    arc(width/2, width/2, size, size, radians(startDegree), radians( endDegree));
    startDegree += angleSize;
  }
}// end drawColorWheel

//Function to create 20 nested colorWheels with saturation gradient 
void satGradientColorWheel( float size){
    bright=100;
    for( int i=100; i>0; i-=5){
      sat = i;
      drawColorWheel(size * i/100.0); 
    }
}

//Function to create 20 nested colorWheels with brightness gradient 
void brightGradientColorWheel( float size){
    sat=100;
    for( int i=100; i>0; i-=5){
      bright = i;
      drawColorWheel(size * i/100.0); 
    }
}
```

