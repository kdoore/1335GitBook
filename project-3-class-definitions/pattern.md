#Pattern

The Pattern class is a wrapper class for geometric shapes that can be displayed at any x,y position.  The shapeColor allows programatic modification of the color.


```java
//add comments here
class Pattern{

  //PROPERTIES
  PShape s ;
  color shapeColor;

  //CONSTRUCTOR 
  //add comments
 
  Pattern( PShape s ,  color shapeColor){
    this.s = s;
    this.shapeColor = shapeColor;
   }
  
  //METHODS
  
  //add comments
  void display(int mx, int my){
    color fillColor = color(hue(shapeColor), saturation(shapeColor), brightness( shapeColor), 50); //set alpha to 100
    s.setFill(fillColor);
    s.setStroke(shapeColor);
    shape(s, mx, my );
  } // end display
 
} // end Pattern class
```

