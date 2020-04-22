---
description: 'Code Wed. Apr 22, 2020'
---

# Code Apr 22

{% tabs %}
{% tab title="Main Tab" %}
```java
//Main Tab
//Make objects, objects call methods

//Global Variables
ButtonGroup btnGroup;  //will hold 4 pattern buttons
Button clearButton;//declare the variable as global - btn is null
color backgroundColor;
color patternFillColor;  //global
color patternStrokeColor; //
//TODO ADD global patternFillColor

Pattern currentPattern; //pointer variable keeps track of active Pattern
Pattern eraserPattern;  //has a PShape circle and background fillColor

//SLIDERS
Slider lengthSlider;

void setup() {
  size( 800, 800);
  colorMode(HSB, 360, 100, 100, 100);
  backgroundColor = color( 300); //light gray
  background( backgroundColor);
 // Button( float x, float y, float w, float h, String label  )
  clearButton = new Button( 10, 450, 100, 100, "Clear");  //initialize - move to bottom
  Button[] btnArray = new Button[4]; //declare and initialize button array
  btnArray[0] = new Button( 10, 10, 100, 100, "Eraser");
  
  PImage img1 = loadImage( "pattern1Btn.png"); //file name with extension
  btnArray[1] = new PImageButton( 10, 120, 100, 100, img1);
  btnArray[2] = new Button( 10, 230, 100, 100, "Pattern2");
  btnArray[3] = new Button( 10, 340, 100, 100, "Pattern3");
  btnGroup = new ButtonGroup( btnArray );
  
  //Logic for patterns
  PShape s0 = createShape( ELLIPSE, 0,0, 50, 50);
  eraserPattern = new Pattern( s0 ); 
  eraserPattern.fillColor = color(backgroundColor);//start with Purple
  eraserPattern.strokeColor = color(backgroundColor);
  currentPattern = eraserPattern;
  
  //Slider(float x, float y, float w, float h, float min, float max, String label ){
  lengthSlider = new Slider( 40,height - 40, 200, 30, 10, 200, "Length");
  
} // end setup

void draw(   ) {
  if( mousePressed){
    checkSliders( );
    translate( mouseX, mouseY );
    displayPattern( ); //draw currentPattern
    resetMatrix();
  }
  displayButtons(); //do after drawing patterns
  displaySliders();
} //end draw

void mouseClicked(   ) {
  boolean isChanged = btnGroup.clicked( mouseX, mouseY);
  if( isChanged){
    changePattern();
  }
  clearButton.clicked( mouseX, mouseY);
  if( clearButton.selected ){
    clearCanvas();
    clearButton.reset();
  }
} //end mouseClicked

void displaySliders(){
  lengthSlider.display();
}//end displaySliders

boolean checkSliders(){
   boolean isChanged = false;
   if(  lengthSlider.checkPressed( mouseX, mouseY)){
     isChanged = true;
   }
   return isChanged;
} //end checkSliders

void changePattern(){
   //TODO add logic to connect buttons to patterns
   //activeBtnIndex will let us determine which pattern should be the currentPattern
   //Switch Case Statement
   float len = 100;  //scale slider will set / modify this value
   
   switch( btnGroup.activeBtnIndex){
      case 0:
          currentPattern = eraserPattern;
      break;
      
      case 1:
          PShape s1 = createShape( RECT, 0,0,len *.8 , len);
          currentPattern = new Pattern( s1);
      break;
      
      case 2:
          PShape s2 = createShape( RECT, 0,0,len , len);
          currentPattern = new Pattern( s2);
      break;
      
      case 3:
          PShape s3 = vertexShape1( len );
          currentPattern = new Pattern( s3 );
      break;
     
     default:
         println("No match on switch case");
     break;
   }  //end switch-case statement
} //end changePattern

void displayPattern(){
  if( currentPattern  != eraserPattern){
    patternFillColor = color( 280, 100, 100, 50);
    patternStrokeColor = color( 0, 50);
    currentPattern.fillColor = patternFillColor;
    currentPattern.strokeColor = patternStrokeColor;
  }
  currentPattern.display();  //sliders will set colors for other patterns
} //end displayPattern

void clearCanvas(){
   //TODO add code to draw a rectangle over the full canvas using background color
  fill( backgroundColor);
  rect( 0,0, width,height);
}//end clearCanvas

void displayButtons(){
  fill(0); //black
  rect( 0,0, 120, height);//background of menu
  btnGroup.display();
  clearButton.display();
} //end displayButtons

//Modify to remove color parameter and color logic
PShape vertexShape1( float len){
  PShape s2 = createShape();
  s2.beginShape( );
  s2.vertex( 0, 0);
  s2.vertex( len * .5, len * .5);
  s2.vertex( len, .7 * len);
  s2.vertex( len * .5, len);
  s2.vertex( 0, len);
  s2.vertex( 0,0);
  s2.beginContour();
  
  s2.vertex( .2 * len, .35 * len);
  s2.vertex( .25 * len, .75 * len);
  s2.vertex( .35 * len, .45 * len);
  s2.vertex( .5 * len, .25 * len);
  
  s2.endContour();
  s2.endShape( CLOSE);
  return s2;
}
```
{% endtab %}

{% tab title="Button" %}
```java
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
//This tab will cause errors, it's missing code
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

{% tab title="Pattern" %}
```java
class Pattern{
   PShape s;
   color fillColor, strokeColor;
   boolean isSvg;  //true if loaded from an external file
   
  Pattern(  PShape s ){
    this.s = s;
  }
  
  void display(){
    if( isSvg){
      //add some fill logic
    }else{  //most of the time
      s.setFill( fillColor);
      s.setStroke( strokeColor); //black by default
      shape( s, 0, 0); //assume translated origin to mouseX, mouseY
    }
  }
  
} //end Pattern class
```
{% endtab %}

{% tab title="Slider" %}
```java
class Slider{
  float x,y;   //position
  float w, h; //size
  String label;
  float min, max;  //end points of range
  
  float sliderX; //mouseX when slider value changes
  float sliderVal; //calculate using the map function 
  
  //CONSTRUCTOR
  Slider(float x, float y, float w, float h, float min, float max, String label ){
    this.x = x;
    this.y = y;
    this.w = w;
    this.h = h;
    this.min = min;
    this.max = max;
    this.label = label;
    
    sliderX = x + w/2.0 ;
    sliderVal = map( sliderX, x, x+w, min, max);
  }
  
  //Behaviors - Methods 
  void backgroundLayer(){
    fill( 200);
    noStroke();
    rect( x-5, y-28,w+10, h+34); //larger than inner slider
    fill(0); //text color
    textAlign( RIGHT);
    textSize(10);
    text( label,x+w, y-16);
  }
  
  void display( ){
    backgroundLayer( );
    fill( 150);
    rect( x,y,w,h);
    //indicator rectangle 
    fill(0);//black
    rect( sliderX-2, y-3, 4, h+6);
    textSize(10);
    text( (int)sliderVal, sliderX+2, y-4);
  }
  
  boolean checkPressed( int mx, int my){
    boolean changed = false;
    if( mx > x && mx < x+w && my> y && my< y+h){ 
      sliderX = mx;
      sliderVal = map( sliderX, x, x+w, min, max);
      changed = true;
    } //end if
    return changed;
  }//end checkPressed
} //end class slider
```
{% endtab %}
{% endtabs %}

