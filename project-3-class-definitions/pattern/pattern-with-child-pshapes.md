###Pattern Class with BrightnessGradient Display of Child PShapes




```java
class Pattern{
   
  PShape s;
  color fillColor;
  color strokeColor;
  
  //simple constructor
  Pattern( PShape s){
    this.s = s;
  }
  
  //overloaded constructor - parameter lists are different and unique
  Pattern( PShape s, color fillColor){
    this.s = s;
    this.fillColor = fillColor;
  }
  
  void display(){
    if( s.getChildCount() > 0){ //special PSHape, has child shapes
      PShape[] children = s.getChildren();
      for( int i=0; i< children.length; i++){
        shape( s, 0,0);
      }
    }else{ //no children
    s.setFill( fillColor); // different ways to set the fill for a PShape
    s.setStroke( strokeColor);
    shape( s, 0,0);
    }
  }
  
  //overloaded method
  void display(int mx, int my){
    s.setFill( fillColor); // different ways to set the fill for a PShape
    s.setStroke( strokeColor);
    shape( s, mx,my);
  }
  
} //end class Pattern
```

