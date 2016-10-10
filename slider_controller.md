# Slider Controller

A slider controller is a user-interface element that we are probably all familiar with.  How can we create our own custom slider controller?  What is the structure, function, behavior of a slider control?

###Structure:
Typically we imagine some horizontal rectangle, with an interactive identifier that show the current position of the slider indicator.

###Function:  
A one dimensional slider is used to determine a value within a given range of values.

###Behavior:
When we press down on the slider, we expect the indicator to move to our mouse position if we are currently positioned over the bar. This is similar to button behavior, the button and slider only change values when they are directly under the mouse and there is some mouse movement. 

###Map: 
Our slider will use the processing map() function because it's core functionality is to provide users with the ability to select a value within a range.  The map function allows us to provide a visual range and an interactive indicator for the user to modify. In code, we create the mapping from the slider tool geometry: w, h, position, to determine the intended variation in the controlled value, such as hue or length. 

![](CS1335 - 9.png)

###Simple Linear Slider
The code below creates a slider that controls the length of a rectangle.  It uses the map function. 
When determining the slider rectangle's range of values, this is determined by the pixel width of the rectangle: w.  In order to determine the values we use to determine the slider's current position and current mapping output value, we need to also consider the x-offset of the slider.  In other words, if the slider's left-side is positioned along the left side of the canvas, then x offset is 0.  This would mean that if the indicator position: sliderX had a value of 20, and if the width of the slider was 40, we'd know that the slider indicator was at the middle of the range.   However, if sliderX had a value of 20, but the x coordinate of the slider rectangle was also 20, we'd know that the slider indicator would be at it's minimum value in the range. Since we want flexibility to position the slider anywhere on the canvas, we need to consider the x offset of the slider when determining the slider's value. So the possible values for the slider Indicator will fall in the range of: ( min: x, max: x+w ), and we'll use these ranges in the map function as the slider representation's min, max value.

###Slider, Base-Class
```
class Slider{
  int x, y, w, h;
  float sliderX;
  float sliderVal;
  float min, max;
  float hue, sat, bright;
  String label;
  
  //initialize default values for sat, bright, and label
  Slider(){
    sat=255;
    bright=255;
    label="";
  }
  
  Slider( int _x, int _y, int _w, int _h,float _min, float _max ){
    x=_x;
    y=_y;
    w=_w;
    h=_h;
    min = _min;
    max = _max;
    sliderX= x + w/2;
    sliderVal = map(sliderX, x, x+w, min, max);
    label="";
  }
  
  //constructor that also takes a label
  Slider( int _x, int _y, int _w, int _h,float _min, float _max, String _label ){
    x=_x;
    y=_y;
    w=_w;
    h=_h;
    min = _min;
    max = _max;
    sliderX= x + w/2;
    sliderVal = map(sliderX, x, x+w, min, max);
    label = _label;
  }
  
  void display(){
    backgroundlayer();
    fill(150);
    rect( x, y, w, h);
    fill(0);
    rect(sliderX-2, y-3, 4, h+6);  
  }
  
  void backgroundlayer(){
    fill(220);
    noStroke();
    rect( x-7, y-20, w+14, h+28);
    fill(0);
    //display SliderVal to 2 decimal digits and Label
    textAlign(LEFT);
    text(nfs(sliderVal,0,2), x,y-7);
    textAlign(RIGHT);
    text(label, x+w, y-6);
  }
  
  void checkPressed(int mx, int my){
    if( mx >= x && mx <= (x+w) && my>=y && my<=(y + h)){
      sliderX = mx;
      sliderVal = map(sliderX, x, x+w, min, max);
      //println("sliderVal " + sliderVal);
    }
  }
  
}
```

###RectanglePattern
```java
class RectanglePattern extends Pattern{
  
  RectanglePattern(){
    super(); //explicitly call Abstract class contructor
  }
  
 void display(){
   scale(scale);
   fill(hue, sat-100, bright-100, alpha-50);  //shadow
   rect(10,10, w, h); //shadow
   fill(hue, sat, bright, alpha);
   rect(0,0, w, h);  //primary pattern
  }
  
}
```
###Main Tab Code: 
In the code below, we use a slider instance to control the scale of an ellipse [PShapePattern](https://kdoore.gitbooks.io/cs1335/content/pshapepattern.html)

```
Slider mySlider;
Pattern rectPattern;

void setup(){
  size(800,800);
  colorMode(HSB);
  
  //////Slider( x, y, w, h, min, max, label);
  mySlider = new Slider( 100,height - 125,250,30, 0.0, 2.0, "Scale"); //we are using this for length
 
  rectPattern = new RectanglePattern();
  background(200);
}

void draw(){
  drawPattern();
  drawSliders();
} // end of draw loop

void drawSliders(){
  if(mousePressed){
    mySlider.checkPressed(mouseX, mouseY);
  }
  mySlider.display();
}

void drawPattern(){
     // base class object reference
      Pattern curPattern = rectPattern;

      /////connect to buttons
       int activeButton=0;
      switch(activeButton){
        case 0:
          curPattern = rectPattern;
        break;
        default:  
      }  //end of switch
  
     if(mousePressed ){
       curPattern.scale = mySlider.sliderVal; //set pattern scale based on slider sliderVal
       translate(mouseX, mouseY);
            curPattern.display();
       resetMatrix();
     } // end if mouse pressed
   } // end of drawPattern 

```
Can you make a slider to control Hue?  Can we use the Slider base class to create a HueSlider class, how do we create a ROYGBIV Gradient Rectangle?
Below is the HueSlider class.  How would we create a Saturation and Brightness slider? 

###HueSlider, Child-class
```
class HueSlider extends Slider{
  
  HueSlider( int _x, int _y, int _w, int _h,float _min, float _max   ){
    super( _x, _y, _w, _h, _min, _max );   ////calling base class constructor
  }
  
  //constructor that also takes a label parameter
  HueSlider( int _x, int _y, int _w, int _h,float _min, float _max, String _label   ){
    super( _x, _y, _w, _h, _min, _max, _label );   ////calling base class constructor
  }
  
  void display(){
    super.backgroundlayer();
    
    for(int i=0;i < w; i ++){  //what's going on here?
      float hue = map( i, 0, w, 0,255);
      stroke(hue, 255,255);
      line(i+x, y , i + x, y + h);
    }
    
    float sliderHue=map(sliderX, x,x+w, 0, 255);
    fill(sliderHue, 255,255);
    stroke(0);
    rect(sliderX, y-4, 5, h+8); 
  }  // end of display
  
} // end of class HueSlider

```