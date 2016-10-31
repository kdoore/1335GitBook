# PShapePattern

If we want to create a pattern class that can be used for creating patterns using any types of PShape, then we need to design a flexible PShapePattern class.  

###Types of PShapes:
There are actually 2 different types of [Processing PShape objects:](https://processing.org/reference/PShape.html)  one type is created by loading a .svg image file.  In that case, we initialize the PShape object using the LoadShape function, example:

```
PShape s = loadShape("myImg.svg"); 
```

The other type of PShape object is created using the Processing primitive shape modes: RECT, etc, or by defining a series of verticies.  For these types of PShapes, we initialize the PShape object using the CreateShape function, example:

```
PShape s = createShape(RECT, 0,0,40,40);
```

When we want to use these PShapes to create a drawing pattern, then we will want to be able to modify the size, shape, and styling of the PShape object.  However, for each different type of PShape object, we need to use slightly different syntax to modify these things.  So, can we create a generalized PShapePattern class that will allow us to use either type of PShape object?  

|  | loadShape(svg) | createShape(vertex), processing primitives |
| -- | -- | -- |
| size | width, height, scale() | scale() |
| style | disableStyle(), fill() | setFill() |

So, we need to create a pattern class that can give us control over these slight variations in syntax.  

Ultimately, we want to use a slider to modify style aspects of the PShape object as we draw patterns on the canvas, so we need variables for each of the style features that we might want modify using a slider.  We have added these [instance variables](https://kdoore.gitbooks.io/cs1335/content/abstract_pattern_class.html#abstract-class-instance-variables) to the abstract base-class: Pattern, because we'll probably want similar control over other custom patterns.  In the code below, we use a boolean: isSvg, to determine whether the PShape object is an Svg type, and in that case, we can specify the styling code to work correctly for each type of PShape object.

How can we set the value of isSvg when we have a PShapePattern instance in our main tab?  Maybe we should create an additional constructor that takes isSvg as an input parameter. 

###PShapePattern Code
```
class PShapePattern extends Pattern{
  PShape s;
  boolean isSvg;
  
  PShapePattern(PShape _s){
   s=_s; 
   isSvg = false;
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
    resetMatrix();
  }
  
} // end of PShapePattern
```

###DisableStyle()
When using an SVG - based PShape, we need to use the  PShape method: disableStyle( ) if we want to modify the fill, stroke of a PShape object, however if we use disableStyle() with a vertex based PShape object, then we will have problems modifying the styles, so we need some approach to solve this problem.  Maybe we should create a boolean field that we use to determine whether s.DisbleStyle() should be called within the display() method, where would we set the value of this boolean field? For example:  boolean isSVG;

