###Button

```java
class Button{
  //instance variables - add comments
  float x, y; //position
  float w, h; //size
  color currentColor, selectedColor, defaultColor;
  boolean selected;
  String label;
  
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
    label = "";
  }
  
  //constructor
  //add comments
   Button(float x,float y,float w,float h, color selectedColor, color defaultColor){
    this.x = x;
    this.y = y;
    this.w = w;
    this.h = h;
    selected = false;
    this.selectedColor = selectedColor;
    this.defaultColor =defaultColor;
    currentColor = defaultColor;
     label = "";
  }
  
  //constructor
  //add comments
   Button(float x,float y,float w,float h, color selectedColor, String label){
    this.x = x;
    this.y = y;
    this.w = w;
    this.h = h;
    selected = false;
    this.label = label;
    this.selectedColor = selectedColor;
    defaultColor = selectedColor;
    currentColor = defaultColor;
  }
  
  //add comments
  void display(){
    fill(currentColor);  //current color is changed when button is clicked
     if( selected){  //set stroke if selected
      stroke(300);
     }
    else{
      stroke(0);
    }
    strokeWeight(3);
    rect( x,y,w,h);
    fill(200);
    textSize(14);
    textAlign(CENTER);
    text( label, x+ (w/2) , y + h/2);
    textAlign(LEFT);
  }
  
  // add comments
  void clicked( int mx, int my){
    if( (mx > x && mx < x + w)  &&( my > y && my < y + h)){
      if( selected==true){  //had been on, now turn off
        selected = false;
        currentColor = defaultColor;
      }
      else{
        selected = true;
        currentColor = selectedColor;
        //println("Selected is true");
      }
    }
  }
}
```

