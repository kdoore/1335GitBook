#Class Code: Sept 9, F19


```java

float sat; //default value 0
float bright; //default value 0

void setup() {
  size( 600, 600);
  colorMode( HSB, 360, 100, 100);
  noStroke();
  sat = 100;
  bright = 100;
}

void draw() {
  background(0);///black background
  float angleSize = map( mouseX, 0, width, 1, 90);
  translate( width/2, height/2); //move origin to center
  satGradientColorWheel(width, angleSize);
  resetMatrix(); //move origin back to upper left
}

//create colorWheels with varying saturation
void satGradientColorWheel(float size, float angleSize ){
  bright=100;
  for( int i=100; i>0; i -=5){
    sat = i; //changing a global variable
    drawColorWheel( (size *i)/100, angleSize); //call the function, pass values as arguments
  }
}


//function to draw an entire color wheel
void drawColorWheel( float size, float angleSize   ) {
  float startDegree =0;
  float endDegree = angleSize;
  float hue = startDegree;
  int numSlices = int(360.0/angleSize); //explicit type-cast
  //loop
  for ( int i= 0; i <= numSlices; i++ ) {
    fill( hue, sat, bright); //hardcode sat, bright 
    arc( 0, 0, size, size, radians(startDegree), radians(endDegree));
    startDegree += angleSize;
    endDegree += angleSize;
    hue = startDegree;
  }
}
```

