# Pattern

The Pattern class is a wrapper class for geometric shapes based on the Processing PShape object. The Pattern display method has x,y postion input parameters to so that the shape can be displayed at any x,y position.  The shapeColor allows programatic modification of the color. The Pattern class allows us to add logic to provide a uniform interface for displaying a variety of PSHape objects, this is necessary because Processing has inconsistent methods for setting the fill and stroke for PShape objects.  We'll expand the logic of this class to handle setting fill for all types of PShape objects.

### Example Usage:

To create a pattern, first create a PShape object, then pass the PShapeObject into the constructor along with a color that will be used for display

```java
//declare as global objects
Pattern pattern1, pattern2, eraserPattern;

//initialize PShape and Pattern in setup
PShape s1 = createShape( RECT, 0,0,40,40);
pattern0 = new Pattern( s1);  //call constructor

//use similar code to initialize all patterns


//display 
pattern0.fillColor = color(100,100,100); //set fill color
pattern0.display( mouseX, mouseY);
```

### Pattern Class Definition

```java
class Pattern{

  //PROPERTIES
   PShape s;
   color fillColor;
   color strokeColor;

  //CONSTRUCTORS
  Pattern( PShape s ){
    this.s = s;
  }

  
  Pattern( PShape s, color fillColor){
    this.s = s;
    this.fillColor = fillColor;
  }
  


  //METHODS
  void display(int mx, int my){
    s.setStroke( strokeColor);
    s.setFill( fillColor);
    shape( s, mx, my);
    } 
}//end PatternClass
```

###Pattern objects for Project 3
For this project, you will create 3 global pattern objects:  

```java
Pattern pattern0, pattern1, eraserPattern;
```

### Initialize in setup  
First you must create 3 PShape objects, then these PShape objects are passed into the Pattern constructor.

```java

//initialize PShape and Pattern in setup
PShape s1 = createShape( RECT, 0,0,40,40);
pattern1 = new Pattern( s1);  //call constructor
```

### Match Patterns to ButtonGroup Buttons in DrawPattern

```java
void drawPattern( ){

Pattern curPattern = pattern0;  //temporary Pattern variable

int activeButton = ButtonGroup.activeButton;

switch( activeButton){
  case 0: //pattern0 and button0
    curPattern = pattern0;
    curPattern.fillColor = color( 50,100,100);
  break;
  
  case 1: //pattern1 and button1
    curPattern = pattern1;
    curPattern.fillColor = color( 150,100,100);
  break;
 
 case 2: //eraser pattern and button
    curPattern = eraserPattern;
    curPattern.fillColor = backgroundColor;
    curPattern.strokeColor = backgroundColor;
 break;

}//end of switch statement logic
//now display the curPattern
  
  curPattern.display( mouseX, mouseY); //display at mouse position
  
}
```



