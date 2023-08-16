# Code Wed Apr 8 v1

During the class demo, the button's colors didn't show correctly.  It was a classic error, it would be nice if I could say I'd planned to make the error, but it was an honest error.  So a good lesson to be learned: &#x20;

The problem was that the colors that were initialized in the constructor were local variables, since I included the dataType:   color.  So, rather than initializing the class instance variables, I created new local variables:  and the instance variables used their default colors of 0,0,0:

```
//Incorrect code in the constructor
 Button( float x, float y, float w, float h, String label  ){
    this.x = x;
    this.y = y;
    this.w = w;
    this.h = h;
    this.label = label;
    
    //the problem is that I created new local variables
    //rather than initializing the class instance variables
    color selectedColor = color( 280, 100, 100); //purple
    color defaultColor = color( 280, 80,70);//dull, dark version
    color currentColor = defaultColor;
    
    selected = false; //button starts in off state
  } //end constructor
```



```
//Correct code in the constructor
Button( float x, float y, float w, float h, String label  ){
    this.x = x;
    this.y = y;
    this.w = w;
    this.h = h;
    this.label = label;
    
    //Correct code:  remove dataType:  color 
    //so that I'm now setting values for instance variables
   selectedColor = color( 280, 100, 100); //purple
   defaultColor = color( 280, 80,70);//dull, dark version
   currentColor = defaultColor;
    
    selected = false; //button starts in off state
  } //end constructor
```

### Full Code:  Main Tab

```
void setup(){
  size( 600, 600);
  colorMode(HSB, 360, 100, 100);
  // Button( float x, float y, float w, float h, String label  )
  btn1 = new Button( 20, 20, 100, 50, "Hello");  //initialize
}

void draw(){
  btn1.display();
  
  fill( color( 280, 100, 100));
  rect( 150, 50, 100 ,50);
  
 }
 
 void mouseClicked(){
   btn1.clicked( mouseX, mouseY);
 }
```

### Class Button - version 1

```
class Button{
  
  //Variables, Properties, Data stored in memory
  float x,y;   //position
  float w, h; //size
  String label;
  
  color selectedColor, defaultColor, currentColor; //HSB
  
  boolean selected;  //false by default
  
  //Constructors
  Button( float x, float y, float w, float h, String label  ){
    this.x = x;
    this.y = y;
    this.w = w;
    this.h = h;
    this.label = label;
    
    selectedColor = color( 280, 100, 100); //purple
    defaultColor = color( 280, 80,80);//dull, dark version
    currentColor = defaultColor;
    
    selected = false; //button starts in off state
  } //end constructor
  
  //METHODS , functions an object can execute for behaviour
  
  void display(  ){
    fill(currentColor);
    //TODO text for label
     rect( x, y, w, h); 
  }
  
   void clicked( int mx, int my){  //mouseX, mouseY
   println("btn has been clicked");
    if( mx > x && mx < x+w && my> y && my< y+h){  //mouse is inside button box
      selected = !selected; //toggle the value 
      if( selected){
        currentColor = selectedColor;
      }else{
        currentColor = defaultColor;
      } //end else
    }//if 
  } //clicked method
    
}//end class
```
