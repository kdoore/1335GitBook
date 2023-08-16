# Slider

## Slider

Slider Base Class

```java
class Slider{
  float x,y;   //position
  float w, h; //size
  String label;
  float min, max;  //end points of range
  
  float sliderX; //mouseX when slider value changes
  float sliderVal; //calculate using the map function 
  
  float hue, sat, bright; //IMPORTANT REMEMBER THESE ALL HAVE VALUE of 0.0
  
  //CONSTRUCTOR
  Slider(float x, float y, float w, float h, float min, float max, String label ){
    this.x = x;
    this.y = y;
    this.w = w;
    this.h = h;
    this.min = min;
    this.max = max;
    this.label = label;
    
    sliderX = x + w/2.0 ;
    sliderVal = map( sliderX, x, x+w, min, max);
  }
  
  //Behaviors - Methods 
  void backgroundLayer(){
    fill( 200);
    noStroke();
    rect( x-5, y-28,w+10, h+34); //larger than inner slider
    fill(0); //text color
    textAlign( RIGHT);
    textSize(10);
    text( label,x+w, y-16);
  }
  
  void display( ){
    backgroundLayer( );
    fill( 150);
    rect( x,y,w,h);
    
    //indicator rectangle 
    fill(0);//black
    rect( sliderX-2, y-3, 4, h+6);
    textSize(10);
    text( (int)sliderVal, sliderX+2, y-4);
  }
  
  boolean checkPressed( int mx, int my){
    boolean changed = false;
    if( mx > x && mx < x+w && my> y && my< y+h){ 
      sliderX = mx;
      sliderVal = map( sliderX, x, x+w, min, max);
      changed = true;
    } //end if
    return changed;
  }//end checkPressed
} //end class slider
```

### Main Tab Code:

In the code below, we use a slider instance to control the scale of an ellipse

```java
Slider slider1;
float hue;   //modified by the slider

void setup(){
  size( 700, 700);
  colorMode( HSB, 360,100,100);
  slider1 = new Slider( 200,200, 200, 30, 0, 360, "Hue");
  hue = slider1.sliderVal;  //initialize hue using slider to set the initial value
}

void draw(){
  background( 0);
   if( mousePressed){
    boolean isChanged = slider1.checkPressed( mouseX, mouseY);
    if(isChanged){
        hue = slider1.sliderVal; //update hue using updated sliderVal
    }
  }
  slider1.display();
  fill( hue, 100, 100); //hue modified by slider1
  rect( 20,20, 50,50); //rectangle hue modified by slider1 
}
```

## HueSlider

For the HueSlider child class, we override the display( ) method. We use a for-loop to draw vertical lines across the rectangle, where each line's color is determined by the map function. The map function calculates what the hueValue should be for each value of i in the for-loop. The for-loop is executed once for every pixel of width in the display's rectangle. So, one line is drawn for every value of i, so map calculates what the hueValue should be, based on i having a range of values from 0-w, where the hueValue should have a range of values from min to max.

```java
class HueSlider extends Slider{
    
  //CONSTRUCTORS
  // Slider(float x, float y, float w, float h, float min, float max, String label ){
  HueSlider(float x, float y, float w, float h, float min, float max){
     super( x, y, w, h, min, max, "HUE");
  }
  
  //METHODS - displays specialized background with ROYGBIV
  void display(){
    super.backgroundLayer(); //call base class method
    for( int i=0; i< w; i++){
      float hueValue = map(i,0,w,min, max);   
      stroke( hueValue, 100, 100);
      line(x+i, y, x+i, y+h); 
    }//end for-loop
    //Indicator rectangle
    //reset stroke
    stroke(0);
    fill(sliderVal, 100, 100);//black
    rect( sliderX-2, y-3, 4, h+6);
    fill(0); //for text
    textSize(10);
    text( (int)sliderVal, sliderX+2, y-4);
    
  }//end display
  
}//end class
```

### SatSlider

The SatSlider also overrides the display( ) method from the base-class. It has logic to determine how the saturation value should change for each vertical line drawn from i=0 to i=w (the width of the rectangle).

```java
class SatSlider extends Slider{
  //no child-class instance variables 

  //base class slider constructor
  // Slider(int x, int y, int w, int h, float min, float max, String label ){

    //Define constructor
    SatSlider( int x, int y, int w, int h, float min, float max  ){
    super(x, y, w, h, min, max, "Sat"  );  //call base-class constructor
  }

  //Draw vertical lines where the saturation changes from min to max
  void display(){
    super.backgroundLayer();
    float satValue = 0;  ///this will be used to color the line
    ///creates saturation varied background of the hitbox rectangle
    for( int i = 0; i< w; i++){
      satValue = map( i, 0, w, min, max); ///convert pixels to colors
      stroke( hue, satValue, 100);
      line( x + i, y, x+i, y+h);
    }
    stroke( 50);
    fill(hue ,sliderVal, 100);
    rect( sliderX-2, y-3, 4, h+6); 
  } //end display

} // end satSlider
```
