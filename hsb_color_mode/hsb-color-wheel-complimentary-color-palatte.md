#HSB Complimentary Color Palette

We can use the Processing function: ` get( x, y);`
to find the HSB color of any pixel on the canvas.  If we combine that with our color-wheel, we can make a simple version of the [Adobe Color Theme tool](https://color.adobe.com/create/color-wheel/).

For any selected pixel, which we identify as having the current color, we can find the complimentary color by finding a hue value on the opposite side of the color-wheel.  

  - First, find the pixel color at the mouse position
  
 `  color curColor = get(mouseX, mouseY); `
  - Find hue, saturation, brightness color components

```java
  float _hue = hue(curColor);
  float _sat = saturation( curColor);
  float _bright = brightness(curColor);
```

  - Find complimentary color by adding 180 degrees to _hue, and use modulus 360 to constrain color values to 0-359 range
  

```
  float _complimentHue = (_hue + 180) % 360;
```

- Finally, create a set of rectangles filled with sat, bright variations of the curColor and complimentHue
   
   
     
#Color Palette Program 
```java

////Global Variables
float sat, bright;
///for initialization
void setup() {
  size( 800, 800);
  colorMode(HSB, 360, 100, 100);
  background(0);
  sat = 100; //initialize to full value saturation
  bright = 100;
  noStroke();
}

void draw() {
  if (mousePressed) { //when mousePressed, show Saturation version
    satGradientColorWheel(600);
  } else { //otherwise show brightness variation version
    brightGradientColorWheel(600);
  }
  //create complimentary colorPalette using get( ) function to find color of pixel at mouse position
  color curColor = get( mouseX, mouseY);
  createColorPalette( curColor, 0, 0); //createColorPalette with currentColor under mouse, at 0,0
}

void createColorPalette(color curColor, int x, int y) {
  float _hue = hue(curColor);
  float _sat = saturation(curColor);
  float complimentHue = (_hue + 180)% 360;
  fill(_hue, _sat * .6, 70); //first one darkest, dullest
  rect( x, y, 100, 100);
  fill(_hue, _sat * .7, 100 );//second one, brighter than first
  rect( x + 100, y, 100, 100);
  fill(curColor);
  rect( x+200, y, 100, 100); //current one in the middle
  fill( complimentHue, _sat, 70); //darker compliment
  rect( x+ 300, y, 100, 100);
  fill( complimentHue, _sat*.8, 100); //lighter compliment
  rect( x+ 400, y, 100, 100);
} //end colorPalette

void satGradientColorWheel( float size) {
  bright=100; //make sure bright and sat start at full values for outer circle
  for ( int i= 100; i>0; i -= 5) {
    sat=i;
    drawColorWheel(size * i / 100.0 );
  }
}

void brightGradientColorWheel(float size) {
  sat=100; //make sure bright and sat start at full values for outer circle
  for ( int i= 100; i>0; i -= 5) {
    bright=i;
    drawColorWheel(size * i / 100.0 );
  }
}

//draws a full color wheel
void drawColorWheel( float size ) {
  float angleSize=10; //declare and intialize local variables
  float startDegree=0; //used for drawing arc, value changes in loop after each arc is drawn
  int numSlices = int(360/angleSize); ///loop maximum value: how many slices to draw?

  for (int i=0; i < numSlices; i++) {
    float endDegree = startDegree + angleSize;
    float hue = startDegree + ( angleSize / 2); //calculate hue for middle of arc
    fill( hue, sat, bright); //set fill
    arc( width/2, height/2, size, size, radians(startDegree), radians( endDegree));
    startDegree += angleSize; //change startDegree for each new slice to be drawn
  }
}

```

