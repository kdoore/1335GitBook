###Button

```java

class Button{
  //instance variables - add comments
  float x, y; //position
  float w, h; //size
  color currentColor, selectedColor, defaultColor;
  boolean selected;
  
  //constructor
  //add comments
  Button(float x,float y,float w,float h){
    this.x = x;
    this.y = y;
    this.w = w;
    this.h = h;
    selected = false;
    selectedColor = color( 225);
    defaultColor = color( 100 );
    currentColor = defaultColor;
  }
  
  void display(){
    fill(currentColor);
    rect( x,y,w,h);
  }
  
  // add comments
  void clicked( int mx, int my){
    if( (mx > x && mx < x + w)  &&( my > y && my < y + h)){
      if( selected){  //turn off
        selected = false;
        currentColor = defaultColor;
        println("Selected is true");
      }
      else{
        selected = true;
        currentColor = selectedColor;
        println("Selected is true");
      }
    }
  }
}
```