#Pattern

The Pattern class is a wrapper class for geometric shapes based on the Processing PShape object. The Pattern display method has x,y postion input parameters to so that the shape can be displayed at any x,y position.  The shapeColor allows programatic modification of the color. The Pattern class allows us to add logic to provide a uniform interface for displaying a variety of PSHape objects, this is necessary because Processing has inconsistent methods for setting the fill and stroke for PShape objects.  We'll expand the logic of this class to handle setting fill for all types of PShape objects.

###Example Usage:
To create a pattern, first create a PShape object, then pass the PShapeObject into the constructor along with a color that will be used for display


```java
//declare as global objects
Pattern pattern1, pattern2;

//initialize PShape and Pattern in setup
PShape s1 = createShape( RECT, 0,0,40,40);
pattern1 = new Pattern( s1, color( 280, 100,100));

//display 
pattern1.display( mouseX, mouseY);
```

###Pattern Class Definition

```java
class Pattern{
  
  //PROPERTIES
   PShape s;
   color shapeColor;
   color strokeColor;
  
  //CONSTRUCTORS
  Pattern( PShape s, color shapeColor){
    this.s = s;
    this.shapeColor = shapeColor;
  }
  
  
  //METHODS
  void display(int mx, int my){
    s.setStroke( strokeColor);
    s.setFill( shapeColor);
    shape( s, mx, my);
    } 
}//end PatternClass
```

