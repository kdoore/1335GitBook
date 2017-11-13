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
The Simple Slider code above has some serious limitations: we can only create a single slider, where it's position and size are fixed.  How can we define a Slider base class that allows us to create a slider of any size, at any position, that allows selection of values within any range?  The map( ) function will allow us to define a more generalized Slider base class. 


```java
class Slider{
  int x, y, w, h;
  float sliderX;
  float sliderVal;
  float min, max;
  float hue, sat, bright;
  String label;


  //constructor with a full set of input parameters
  Slider( int x, int y, int w, int h,float min, float max, String label ){
    this.x=x;
    this.y=y;
    this.w=w;
    this.h=h;
    this.min = min;
    this.max = max;
    sliderX= x + w/2;
    sliderVal = map(sliderX, x, x+w, min, max);
    this.label = label;
    sat = 255;
    bright = 255;
    hue = 0;
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
    text(int(sliderVal), x,y-7);
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

}// end class
```


###Main Tab Code: 
In the code below, we use a slider instance to control the scale of an ellipse 

```java
Slider mySlider;


void setup(){
  size(800,800);
  colorMode(HSB);
  
  //////Slider( x, y, w, h, min, max, label);
  mySlider = new Slider( 100,height - 125,250,30, 0.0, 2.0, "Scale"); //we are using this for length
 background(200);
}

void draw(){
  if(mousePressed){
  drawPattern();
  }
  drawSliders();
} // end of draw loop

void drawSliders(){
  if(mousePressed){
    mySlider.checkPressed(mouseX, mouseY);
  }
  mySlider.display();
}

void drawPattern(){
   
   
   } // end of drawPattern 

```
Can you make a slider to control Hue?  Can we use the Slider base class to create a HueSlider class, how do we create a ROYGBIV Gradient Rectangle?
Below is the HueSlider class.  How would we create a Saturation and Brightness slider? 

###HueSlider, Child-class
```java
class HueSlider extends Slider{
  
  HueSlider( int _x, int _y, int _w, int _h,float _min, float _max   ){
    super( _x, _y, _w, _h, _min, _max, "HUE" );   ////calling base class constructor
  }
  
 
  void display(){
    super.backgroundlayer();
    
    for(int i=0;i < w; i ++){  //what going on here?
      float hue = map( i, 0, w, min, max);  //what is wrong here, what should be used instead of 0, 255 for slider min, max range?
      stroke(hue, 255,255);
      line(i+x, y , i + x, y + h);
    }
    
    float sliderHue=map(sliderX, x,x+w, 0, 255);  //what is wrong here?
    fill(sliderHue, 255,255);
    stroke(0);
    rect(sliderX, y-4, 5, h+8); 
  }  // end of display
  
} // end of class HueSlider

```

To create Saturation and Brightness sliders, we need to consider that their display may be dependent on the Hue slider.  So, in the main tab of our project, When we check the HueSlider, and before we display the Bright or Sat Sliders, we can use the value of the HueSlider to set their hue attribute.

//in main tab:

void CheckSliders(){
    

}

//SAT SLIDER

```java
class SatSlider extends Slider{
  
  SatSlider(int _x, int _y, int _w, int _h, float _min, float _max){
    super( _x, _y, _w, _h, _min, _max);
    }
  
  void display(){
    super.drawBackground();
    for( int i=0; i < w ; i++){
      float satVal = map( i, 0,w, min, max);  //changed
      stroke( hue, satVal, 255); //calculate satVal for each line
      line( x+i, y, x+i, y+h); 
    }
    ///indicator rectangle
    stroke(0);  //reset stroke to default
    fill(hue , sliderVal,255);   //use sliderVal to set the sat 
    strokeWeight(2);
    rect( sliderX-3, y-2, 6, h+4);
    strokeWeight(1);
  }
   
  
} // end of class
```

###Main Tab Code
Here's how we check the sliders and use the Hue Slider to set the hue value for the SatSlider before we display the SatSlider.

```java

void drawSliders(){
  slider.display();
  hueSlider.display();
  satSlider.hue = hueSlider.sliderVal;  //before drawing sat slider, update hue value
  satSlider.display();
}

void checkSliders(){
   slider.checkPressed(mouseX, mouseY);
   hueSlider.checkPressed(mouseX, mouseY);
   satSlider.checkPressed(mouseX, mouseY);
   }

```