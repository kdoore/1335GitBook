#PShapes - SVG and Vertex Shapes

Setting the fill and stroke for PShapes is non-trivial since the PShape class is a wrapper class that tries to treat several different types of shapes as the same type.  

We can make modifications to the Pattern class to help smooth out these difficulties.

The Noun Project  [https://thenounproject.com/](https://thenounproject.com/)
Provides an easy way to get some simple svg's that we can use to create patterns.

#Table of Fill, Stroke Syntax for PShapes


|  PShape |  Type |   Fill Syntax |
| ------- | ----- | -----|
|  s = createShape( RECT,0,0,20,40)| processing primitive | s.setFill(color( 100) ); |
|  s = createShape( ); | vertex shape | s.setFill(color(100) ); |
|  s = loadShape("shape.svg" )| external svg file | s.disableStyle( ); fill(color(100) ); |


## Updated Pattern Class - For All PShapes

The code below can be used with all types of PShapes. When using the external svg version, you must set the value of isSVG = true  in the main tab after creating the Pattern object.

**example main tab code**
 

```java
 PShape s1 = loadShape( "nounPattern.svg");
  pattern1 = new Pattern(s1);
  pattern1.isSVG = true;
  pattern1.fillColor = color( 200, 100, 100);
  pattern1.display();
```

###Pattern Class

```java
class Pattern{
  //Properties
  PShape s;
  color fillColor;
  color strokeColor;
  boolean isSVG;  //false by default - set to true for external loaded files
  
  Pattern(  PShape s ){
    this.s = s;
  }
  
  //overloaded constructors
  Pattern(  PShape s, color fillColor ){
    this.s = s;
    this.fillColor = fillColor;
  }
  
  void display(){
    if(isSVG){
      s.disableStyle();
      fill( fillColor);
      stroke(strokeColor);
    }else{
    //fill( fillColor);
    s.setFill( fillColor);
    s.setStroke( strokeColor);
    }
    shape( s,0,0);
  }//end display
  
}  //end class Pattern

```

