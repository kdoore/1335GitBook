### PShapePattern

If we want to create a pattern class that can be used for creating patterns using any types of PShape, then we need to design a flexible PShapePattern class.  

###Types of PShapes:
There are actually 3 different types of [Processing PShape objects:](https://processing.org/reference/PShape.html)  one type is created by loading a .svg image file.  In that case, we initialize the PShape object using the LoadShape function, example:

```
PShape s = loadShape("myImg.svg"); 
```

The other types of PShape objects are created using the Processing PShape function createShape(). There are 2 basic types of these PShapes, the first type are created primitive shape modes: RECT, ELLIPSE, etc.  The second type are created defining a series of verticies.  For both of these types of PShapes, we initialize the PShape object using the CreateShape function, example:

```
PShape s = createShape(RECT, 0,0,40,40);
```

When we want to use these PShapes to create a drawing pattern, then we will want to be able to modify the size, shape, and styling of the PShape object.  However, for each different type of PShape object, we need to use slightly different syntax to modify these properties.  So, can we create a generalized PShapePattern class that will allow us to use either type of PShape object?  

|  | loadShape(svg) | createShape(vertex), processing primitives |
| -- | -- | -- |
| size | width, height, scale() | scale() |
| style | disableStyle(), fill() | fill, setFill() |

So, we need to create a pattern class that can give us control over these slight variations in syntax.  

Ultimately, we want to use a slider to modify style aspects of the PShape object as we draw patterns on the canvas, so we need variables for each of the style features that we might want modify using a slider.  We have added these [instance variables](https://kdoore.gitbooks.io/cs1335/content/abstract_pattern_class.html#abstract-class-instance-variables) to the abstract base-class: Pattern, because we'll probably want similar control over other custom patterns.  In the code below, we use a boolean: isSvg, to determine whether the PShape object is an Svg type, and in that case, we can specify the styling code to work correctly for each type of PShape object.

How can we set the value of isSvg when we have a PShapePattern instance in our main tab?  Maybe we should create an additional constructor that takes isSvg as an input parameter. 

###PShapePattern Code
```
class PShapePattern extends Pattern{
  PShape s;
  boolean isSvg; //how can we set this value?  we can only set it using a constructor, since it's not part of the Pattern base class.
  
  PShapePattern(PShape _s){
  this(_s, false);
  }
  
   PShapePattern(PShape _s,boolean _isSvg){
   s=_s; 
   isSvg = _isSvg;
  }
  
  void display(){
    if(isSvg){
    s.disableStyle();  //causes problems when used to style createShape-pShapes based
    fill(color(hue, sat, bright , alpha));
    noStroke();
    }
    else{
     s.setFill(color(hue, sat, bright , alpha));
    }
    
    scale(scale);
    shape(s , 0 , 0);
    resetMatrix();  //remove scale transformation
  }
  
} // end of PShapePattern
```

###DisableStyle()
When using an SVG - based PShape, we need to use the  PShape method: disableStyle( ) if we want to modify the fill, stroke of a PShape object, however if we use disableStyle() with a vertex based PShape object, then we will have problems modifying the styles, so we need some approach to solve this problem.  Maybe we should create a boolean field that we use to determine whether s.DisbleStyle() should be called within the display() method, where would we set the value of this boolean field? For example:  boolean isSVG;

However, we must be aware that we can only set the value of isSvg using the constructor, since we aren't defining it in the Pattern base class.  Typically we want to use a base class object reference, but that means that we can only call methods and properties that are defined in the Pattern base class.

```java
Pattern myPattern;
PShape s = loadShape("Monster.svg");
myPattern = PShapePattern(s);

///incorrect
myPattern.isSvg = true;  ////this will cause an error since Pattern doesn't have isSvg as an instance variable.

//instead we must call the correct constructor:
myPattern = PShapePattern(s, true);  //sets isSvg = true 


```
###DrawPattern()



```java


void drawPattern(){
  translate(mouseX, mouseY);
  int myMenuArrayActiveButton = 0;
  Pattern curPattern = p1;  ///problem if not initialized
  switch(myMenuArrayActiveButton){
    case 0:
       curPattern = p1;
    break;
    
    case 1:
       curPattern = p2;
    break;
    
    default:
      println("No match on switch case");
    break;
    
  }
  curPattern.scale = slider.sliderVal;
  curPattern.hue = hueSlider.sliderVal;
  //curPattern.sat = satSlider.sliderVal;
  //curPattern.bright = brightSlider.sliderVal;
  curPattern.display();
  
  resetMatrix();
}
```





