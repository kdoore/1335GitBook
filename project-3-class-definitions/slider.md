#Slider

Slider Base Class

```java
//Class slider 
//creates a horizontal slider
//uses map function to match displayed slider rectangle and 
//indicatror rectangles with the min, max values provided as input parameters
class Slider {
  float x, y;
  float w, h;
  float min, max;
  float sliderX;
  float sliderVal;
  String label;
  float hue, sat, bright; //used for child class sliders
 

  Slider( float x, float y, float w, float h, float min, float max, String label) {
    this.x = x;
    this.y = y;
    this.w = w;
    this.h = h;
    this.min = min;
    this.max = max;
    this.label = label; 
   
    sliderX = x + (w/2); //pixel location of slider midpoint
    sliderVal = map( sliderX, x, x+w, min, max); //mapped value associated with midpoint initialization
    
  }

  //display split into 2 methods, the background layer display can be used for child classes
  void display() {
    backgroundLayer();

    fill(300);
    rect( x, y, w, h);   //slider rectangle  - this is changed in child classes 

    fill(360); //indicator rectangle
    rect( sliderX-2, y-3, 4, h + 6);
    text( int(sliderVal), sliderX + 2, y-4);  //display the sliderValue
  }
  
  
  //display background rectangle that has text display 
  //for min, max, label
  //can be used in child classes
  
  void backgroundLayer() {
   
    fill( 100); 
    rect( x-10, y-20, w+20, h+40);  ////outer background rectangle
    fill( 360);  //fill for the text
    // Create text for min, max, label - displayed under slider rectangle
    textSize( 12);
    textAlign(LEFT);  //display min at left
    text( int(min), x, y+h+15);
    textAlign(RIGHT); //display max at right
    text( int( max), x+w-10, y+h+15);
    
    textAlign(CENTER);
    textSize(14);
    text( label, x+(w/2), y+h +15);
  
  }

 
  //test mouse coordinates to determine if within the slider rectangle
  //if not changed, return false
  //set sliderX to current mouseX position
  boolean checkPressed(int mx, int my) {
    boolean isChanged = false;
    if ( mx >= x && mx <= x+w && my> y && my< y +h) { //test for >= so endpoints are included
      isChanged = true;
      sliderX = mx;
      sliderVal = map( sliderX, x, x+w, min, max);
    }
    return isChanged;
  }
} // end class Slider
```

###Main Tab Code: 
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

