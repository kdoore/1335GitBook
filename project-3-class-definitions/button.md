###Button


```java
class Button{
  
  //PROPERTIES
  
  //instance variables - add comments
  float x, y; //position
  float w, h; //size
  color currentColor, selectedColor, defaultColor;
  boolean selected;
  String label;
  
  //CONSTRUCTORS
  
  //add comments
   Button(float x,float y,float w,float h, color defaultColor, color selectedColor, String label){
    this.x = x;
    this.y = y;
    this.w = w;
    this.h = h;
    selected = false;
    this.selectedColor = selectedColor;
    this.defaultColor = defaultColor;
    currentColor = defaultColor;
    this.label = label;
  }
  
  //add comments
  //button with a single color and a label
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
  
  //METHODS
  
  // add comments
  void display(){
    pushStyle();
    fill(currentColor);
     if( selected){
      stroke(200);
     }
    else{
      stroke(0);
    }
    strokeWeight(3);
    rect( x,y,w,h);
    fill(150);  //text color
    textSize(16);
    textAlign(CENTER);
    text( label, x+ (w/2) , y + h/2);
    textAlign(LEFT);
    popStyle();
  }
  
  void updateColor(color selectedColor, color defaultColor){
    this.selectedColor = selectedColor;
    this.defaultColor =defaultColor;
    currentColor = defaultColor;
  }
  
  //sets the button to be on
  void setActive(){
       selected = true;
       currentColor = selectedColor;
    }
  
  //sets the button to be off
  void reset( ){
    this.selected = false;
    currentColor = defaultColor;
  }
  

  // add comments
  void clicked( int mx, int my){
    if( (mx > x && mx < x + w)  &&( my > y && my < y + h)){
      if( selected==true){  //if it had been on, now turn off
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
} // end class Button
```

