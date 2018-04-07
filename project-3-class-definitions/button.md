###Button
For this project, you will create 4 buttons.  1 Button, the clearButton, will be a basic Button using the constructor to set the x, y, w, h for the button's position and size, and then specifying 2 colors and a String, label, that's used to display text on the Button.  You will also define a child class, either PImageButton or PShapeButton so you can create Buttons that display an image.

###Example Use



```java
//Button Constructor showing parameter details
//Button( int x, int y, int w, int h, color c1, color c2, String label)

Button button1 = new Button( 10, 10, 100, 100, color1, color2, "Button1");

//display the button
button1.display();

//click the button
button1.click( mouseX, mouseY);

```


###Class Code

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

