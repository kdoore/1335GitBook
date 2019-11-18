###Pattern Class with BrightnessGradient Display of Child PShapes


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
        float fraction = map( i, 0, children.length, 1.0, 0.5);
        color curColor = color( hue(fillColor), saturation(fillColor), brightness( fillColor) *fraction);
        s.setFill( curColor);
        s.setStroke( strokeColor);
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