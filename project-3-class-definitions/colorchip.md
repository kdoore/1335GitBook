#ColorChip

The ColorChip class creates an object that contains a button 

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
    pushStyle();
    strokeWeight(3);
    if (button.selected) {
      stroke(200);
    } else {
      stroke(0);
    }
    fill(50);
    rect( x, y-2, w-2, h+32);
    String label = String.format( "%1$.0f, %2$.0f, %3$.0f", hue, sat, bright);
    fill(150); //text color
    textSize(12);
    text( "HSB:" + label, x+5, y+h+20 );
    button.display();
    popStyle();
  }
}// end class ColorChip
```

