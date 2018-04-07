###Setting Colors for Patterns

Since this project requires programmatic use of colors, we need to look at how to set the colors for each Pattern object.  One way to set the color is to pass a color parameter into a Pattern constructor, but in that case, the color would not be dynamic, it would not change when the mouse is moved.  


Using this constructor, we can pass in a color parameter, so the color is fixed when the object is created.

###Example Use

```java 

///In Pattern class definition
//Pattern constructor that takes color as an input parameter
Pattern( PShape s, color fillColor){
    this.s = s;
    this.fillColor = fillColor;
  }

//main tab - initialization in setup()
PShape shape1 = createShape( RECT, 0,0,40,80);
color color1 = color( 200,100,100);
Pattern pattern0 = new Pattern(shape1, color1);

//in drawPattern( )
pattern0.display(mouseX, mouseY); //displayed using color1
```

###Dynamic Color
To have dynamic color change for the Pattern objects, we can just modify the value for the Pattern object's variables: fillColor or strokeColor, right before we call the display( ) method.


