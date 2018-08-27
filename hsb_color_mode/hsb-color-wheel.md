#HSB Color-Wheel
The images below show 2 color wheels, both color-wheels have an outer ring of full saturation and brightness.  The first color-wheel has saturation reduced toward the center.  The second color-wheel has brightness decreased toward the center.  

![Decreased Saturation](/assets/Screen Shot 2018-08-27 at 6.55.00 AM.png) ![Decreased Brightness](/assets/Screen Shot 2018-08-27 at 6.53.34 AM.png)


```java

//Global variables
int startDegree = 0;
int angleSize = 10;

int hue = 0; //start with Red 
int sat = 100; //start with full saturation
int bright = 100; //start with full brightness

//initialize
void setup() {
  size( 400, 400);
  colorMode(HSB, 360, 100, 100); //Hue range 0-360, Sat, Bright range 0-100
  background(0); //black
  noStroke();
 
} //end setup


void draw(){
  sat = 100;
  bright=100;
  drawColorWheel(width);
  
  //draw inset wheels with reduced saturation
  sat = 85;  //reduce saturation
  drawColorWheel(width * .75);
  sat = 75; //reduce saturation
  drawColorWheel(width * .5);
  sat = 50; //reduce saturation
  drawColorWheel(width * .25);
  sat = 25; //reduce saturation
  drawColorWheel(width * .075);
 
}

//Function to draw colorwheel, input size of colorwheel
void drawColorWheel(float size) {
  int numSlices = 360/angleSize; //how many to draw - should be an int
  //loop to draw color arcs to cover full 360 degrees
  for (int i=0; i< numSlices; i++) {
    hue = (startDegree + (angleSize/2))%360 ; //modulus keeps hue in range <=360
    fill(hue, sat, bright);
    int endDegree = startDegree + angleSize;
    arc( width/2, height/2, size, size, radians(startDegree), radians( endDegree));
    
    //change startDegree for next arc
    startDegree =(startDegree + angleSize);
  } //end for-loop
} //end function


```

