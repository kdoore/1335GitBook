#ColorChip
The ColorChip class creates an object that represents a selectable color button, the ColorChip class is designed to be used in conjunction with the ColorScheme class, where a selectable ColorChip object is created for each color array element. 

###Example Usage
ColorChips can be created independently, or they can be created as part of a ColorScheme object.  Each ColorChip displays it's chipColor, it also displays it's HSB component values.  This class can be expanded to include sliders to allow programatic modification of the ColorChip's chipColor.

///Example creation based on an array of colors, created inside the colorScheme constructor:


###ColorChip Class Definition


```java
class ColorChip {

  //PROPERTIES
  
  //add comments
  Button button;
  float hue, sat, bright;
  float x, y, w, h;
  color chipColor;
  int index;

  //CONSTRUCTORS
  
  //default constructor -  add comments 
  ColorChip( float x, float y, float w, float h, color chipColor, int i) {
    this.x = x;
    this.y = y;
    this.w = w;
    this.h = h;
    this.chipColor = chipColor;
    this.index = i;
    hue = hue(chipColor);
    sat = saturation(chipColor);
    bright = brightness(chipColor);
    button = new Button(x, y, w-3, h, chipColor, "C" + i);
  }

  //METHODS
  
  //add comments
  void display() {
    pushStyle();   //save prior styles
    strokeWeight(3);
    if (button.selected) {   //set stroke if selected
      stroke(200);
    } else {
      stroke(0);
    }
    fill(50);
    rect( x, y-2, w-2, h+32);  //background square 
    String label = String.format( "%1$.0f, %2$.0f, %3$.0f", hue, sat, bright);
    fill(150); //text color
    textSize(12);
    text( "HSB:" + label, x+5, y+h+20 );  //display HSB values
    button.display();
    popStyle();   //restore prior styles
  }
}// end class ColorChip
```

