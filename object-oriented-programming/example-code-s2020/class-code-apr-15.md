# Class Code Apr 15

**Main Tab Code:** Created PImageButton

**Button:** Added reset\( \) method

**ButtonGroup:** Created Class Code

**PImageButton:** Child Class of Button, Added Constructor logic, display\( \) method

{% tabs %}
{% tab title="Main Tab" %}
```text
//Main Tab
//Make objects, objects call methods

//Make an object instance

Button btn1;//declare the variable as global - btn is null

void setup(){
  size( 600, 600);
  colorMode(HSB, 360, 100, 100);
  
  PImage img1 = loadImage( "pattern1Btn.png");
  //image( img1, 100, 100);  //test to make sure you can display image
  
  // Button( float x, float y, float w, float h, String label  )
  btn1 = new PImageButton( 20, 20, 100, 100, img1);  //initialize
}

void draw(   ){
  btn1.display();
 }
 
 void mouseClicked(   ){
   btn1.clicked( mouseX, mouseY);
 }
```
{% endtab %}

{% tab title="Button" %}
```text
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
    defaultColor = color( 280, 70,50);//dull, dark version
    currentColor = defaultColor;
    
    selected = false; //button starts in off state
  } //end constructor
  
  //METHODS , functions an object can execute for behaviour
  
  void display(  ){
    fill(currentColor);
    rect( x, y, w, h); 
    fill(0); //set fill to black
    textAlign(CENTER); //x,y specifies center line of text
    text( label, x+ w/2.0, y+ h/2.0 + 10);
  }
  
   void clicked( int mx, int my){  //mouseX, mouseY
    if( mx > x && mx < x+w && my> y && my< y+h){  //mouse is inside button box
      selected = !selected; //toggle the value 
      //println("btn has been clicked, selected value " + selected);
      if( selected){
        currentColor = selectedColor;
      }else{
        currentColor = defaultColor;
      } //end else
    }//if 
  } //clicked method
  
  void reset(){
    selected = false;
    currentColor = defaultColor;
  }
    
}//end class
```
{% endtab %}

{% tab title="ButtonGroup" %}
```java
class ButtonGroup{
  //Properties - data
  Button[] buttons;
  int activeBtnIndex;
  
  //Constructor
  ButtonGroup( Button[] buttons ){
    this.buttons = buttons;
    activeBtnIndex = 0;  //first button is 'active' it is the eraser
  }
  
  //Methods
  void display(){
     for( int i=0; i< buttons.length; i++){
       buttons[i].display();
      } //end for
  } //end display
  
  //returns true if a button has been changed to active state
  boolean clicked( int mx, int my ){
      boolean isChanged = false;
        for( int i=0; i< buttons.length; i++){  //for every button - outer loop
          if( buttons[i].selected == false){  //this button is not currently active
              buttons[i].clicked( mx, my);
              if( buttons[i].selected == true){
                activeBtnIndex = i;
                isChanged = true;
                for( int j=0; j< buttons.length; j++){
                  if( i != j){  //not the current button
                    buttons[j].reset();
                  } //end if
                } //end inner loop
              }//end if selected is true
           }//end if selected is false
      } //outer loop  
    return isChanged;
  } //end clicked
  
  
}//end class
```
{% endtab %}

{% tab title="PImageButton" %}
```java
class PImageButton extends Button{
  //Variables - Data
  PImage img;
 
  //CONSTRUCTORS
  //Button( float x, float y, float w, float h, String label  )
  PImageButton( float x, float y, float w, float h, PImage img ){
    super( x, y, w,h,"" );  //call to base class constructor
    this.img = img;
    } //end constructor
  
  //METHODS - Behaviours
  void display(  ){
    super.display(); //call the base class method
    image( img, x+10, y+10, w-20, h-20);
  }
  
} //end class
```
{% endtab %}
{% endtabs %}

