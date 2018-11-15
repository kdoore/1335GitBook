###Setting Colors for Patterns

Since this project requires programmatic use of colors, we need to look at how to set the colors for each Pattern object.  One way to set the color is to pass a color parameter into a Pattern constructor, but in that case, the color would not be dynamic, it would not change when the mouse is moved.  


Using this constructor, we can pass in a color parameter, so the color is fixed when the object is created.

###Example Use - Fixed Color

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

###Example Use - Dynamic Color
To have dynamic color change for the Pattern objects, we can just modify the value for the Pattern object's variables: fillColor or strokeColor, right before we call the display( ) method.  


```java

//main tab - initialization in setup()
colorMode(HSB, 360,100,100);
PShape shape1 = createShape( RECT, 0,0,40,80);
color color1 = color( 200,100,100);
Pattern pattern0 = new Pattern(shape1, color1);

//in drawPattern( )
float hue = map( mouseX, 0, width, 100, 200);  //vary with mouse position with colors in a hue range fo 100-200
pattern0.fillColor = color( hue, 100, 100 ); //set fillColor before calling display method.
pattern0.display(mouseX, mouseY); //displayed using color1

```

###Pattern Class that handles all types of PShapes
This version of the Pattern class introduces a PShapeType integer variable, this allows us to customize the logic in the display method depending on the type of PShape Object we're dealing with:  


```java
class Pattern{
   
  //PROPERTIES
  PShape s;
  color shapeColor, strokeColor;
  int PShapeType; //type 1, type 2, type 3
  //type 1:  vertex type
  //type 2:  processing primitive
  //type 3:  external .svg file
  
  //CONSTRUCTOR
  Pattern( PShape s, color shapeColor){
    this.s = s;
    this.shapeColor = shapeColor;
    PShapeType = 1;  //default, assume vertex type
  }
  
  Pattern( PShape s, color shapeColor, int type){
    this.s = s;
    this.shapeColor = shapeColor;
    PShapeType = type;
  }
  
  
  //METHODS
  void display( int mx, int my){
   if( PShapeType == 1){
   s.setFill( shapeColor);
   s.setStroke(strokeColor);
   }
   else if( PShapeType == 2){
     fill(shapeColor);
     stroke(strokeColor);
   }
     shape( s, mx, my );
  }
  
}

```


