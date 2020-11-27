# Particles

### Class Particle

Code below modified from Shiffman's Nature of Code

```java
//From Shiffman, Nature of Code, Chapter 4
//Modified to use PShape and to modify color: HSB with particle age
class Particle {
//Particle has location, velocity, and acceleration, PShape, color, lifespan
  PVector location;
  PVector velocity;
  PVector acceleration;
  float lifetime, lifespanMax;
  PShape s;
  color c;

  //CONSTRUCTOR
  Particle(PVector l, PShape s, color c) { //create particle at location: l
    location = new PVector(); //initailize PVector
    location.set(l);  //set location with parameter l
    this.s=s ;
    this.c = c;
//For demonstration purposes we assign the Particle an initial velocity and constant acceleration.
    acceleration = new PVector(0,random(0.1, .05));
    velocity = new PVector(random(-.5,1),random(-2.5,0));

    lifespanMax = random( 50, 100);
    lifetime = lifespanMax;
  }

  void update() {
    velocity.add(acceleration);
    location.add(velocity);
    lifetime -=1;
  }

  void display() {
    //Use changing lifetime compared to lifespanMax - to change brightness and hue
    if( s.getChildCount()==0){ //change fill if PShape does not have children
      float fractionDecr = map( lifetime, lifespanMax/2, 0, 1.0 ,random( 0.6, .2));
      float fractionIncr = map( lifetime, lifespanMax, 0, 0.8 ,1.0);
      s.setFill( color(hue(c)*fractionIncr, saturation(c)*fractionIncr, brightness( c) * fractionDecr));
    }
    shape(s, location.x, location.y);
  }

  void run() {
    update();
    if( frameCount %2 == 0){ //don't display every frame, use modulus to give pause
        display();
    }
  }


  boolean isDead() {
//Is the particle still alive?
    if (lifetime < 0.0) {
      return true;
    } else {
      return false;
    }
  }
}
```

### Class Particle System

```java
import java.util.Iterator;

class ParticleSystem {
//One list, for anything that is a Particle or extends Particle

  ArrayList<Particle> particles;
  PVector origin;

  ParticleSystem(PVector location) {
    origin = new PVector();
    origin.set(location);
    particles = new ArrayList<Particle>();
  }

  void addParticle(PVector location, PShape s, color c) {

   Particle particle = new Particle( location, s, c);
   particles.add(particle);

  }


  void run() {
    Iterator<Particle> it = particles.iterator();
    while (it.hasNext()) {
//Polymorphism allows us to treat everything as a Particle, whether it is a Particle or a Confetti.
      Particle p = it.next();
      p.run();
      if (p.isDead()) {
        it.remove();
      }
    }
  }
}
```

## Example Main-Tab Code:

Requires use of All Project 3 Classes. The main-tab code has been refactored in several ways to

```java
Button clearButton, particleButton;   //data-type, variable-name   //null

color bkgColor, globalColor;  //global since used in several different functions
ParticleSystem ps;
ButtonGroup btnGroup;  //will refer to a ButtonGroup object instance
Pattern curPattern;

Pattern pattern1, pattern2, pattern3, eraserPattern; ///4 patterns to match 4 buttons
Slider hueSlider, satSlider, brightSlider, lengthSlider; //base-class variable type

///Initialize things - variables
void setup(){
  size( 1000, 800);
  colorMode(HSB, 360, 100, 100);

  bkgColor = color(50);//dark gray
  background( bkgColor);///sets the background once with bkgCOlor
  //Initialize Pattern Objects 
  //Place-holder PShapes
  ps = new ParticleSystem(new PVector(width/2,50)); //starting position

  PShape s0 = createShape( ELLIPSE, 0,0,10, 10); //this is fine
  //Call constructors to create the objects
  eraserPattern = new Pattern( s0, bkgColor);  //pattern0
  eraserPattern.strokeColor = bkgColor;
  curPattern = eraserPattern;
  //the image named below must be in a folder named 'data' 
  //that you will create inside your sketch folder
  PImage img1 = loadImage("pattern1Btn.png" );
   PImage img3 = loadImage("btn3Img.png" );
  ///image( img1, 200,200); //test the image
  clearButton = new Button( 10, 10, 100, 100, "Clear" );  //initialize by calling a Button constructor
  particleButton = new Button( 10, 600, 100, 100, "Particles"); 
   //local variable - we use the ButtonGroup instead of the btnArray in program
   Button[] btnArray;  //declare the variable - of the Base-class type: Button  //null
   btnArray = new Button[4]; //initialize the array so it has 3 button elements
   // PImageButton(float x, float y, float w, float h, PImage img)
   btnArray[0] = new Button( 10, 120, 100, 100, "Eraser" ); 
   btnArray[1] = new  Button( 10, 230, 100, 100, "Btn1" );
   btnArray[2] = new Button( 10, 340, 100, 100, "Btn2" );
   btnArray[3] = new  Button( 10, 450, 100, 100, "Btn3");
   btnGroup = new ButtonGroup(btnArray); //Call constructor for ButtonGroup, pass in array
   //initialize sliders
   hueSlider = new HueSlider( 140, 700,  150, 40, 100, 260);

   satSlider = new SatSlider( 380, 700, 150, 40, 0, 100);
   satSlider.hue = hueSlider.sliderVal;
   brightSlider = new Slider( 620, 700, 150, 40, 0, 100, "Bright");
   lengthSlider = new Slider( 850, 700, 130, 40, 0.0, 2.0, "Scale");

//call checkSliders()
//call changePatternColor();
}//in setup

//makes it a frame-based application
void draw( ){
 if(mousePressed){
   if( particleButton.selected){  //when particleButton is active
    ps.addParticle(new PVector( mouseX,mouseY), curPattern.s, globalColor);
   }
    if(checkSliders()){ //check if sliders have been changed
       changePattern();
    }
    pushMatrix();
    translate( mouseX, mouseY);
    displayPattern();
    popMatrix();
   }
   ps.run(); //particle display - animation happens here

  displayButtons();
  displaySliders();
}

void mouseClicked( ){
  clearButton.clicked( mouseX, mouseY);
  particleButton.clicked( mouseX, mouseY);
  if( clearButton.selected){
    clearCanvas();
    clearButton.reset(); //turn off like a doorbell
  }
  if(btnGroup.clicked( mouseX, mouseY)){
    changePattern();
  }
}

void displaySliders(){
  fill( 0); //draw black background rectangle
  rect( 120, 650, width, height - 650);
  hueSlider.display();
  satSlider.display();
  brightSlider.display();
  scaleSlider.display();
}

boolean checkSliders(){
 boolean changed = false;
  if(hueSlider.checkPressed( mouseX, mouseY)){
    changed = true;
    satSlider.hue = hueSlider.sliderVal;
    brightSlider.hue = hueSlider.sliderVal;
    changePatternColor();
  }
  //add logic for other color sliders 
if( lengthSlider.checkPressed(mouseX, mouseY)){
    changed = true;
  }
 return changed;
}

void changePatternColor(){
  globalColor = color( hueSlider.sliderVal, 100, 100); //color using al colors
 }

//Contains logic to connect ButtonGroup buttons to control which patterns is drawn
void changePattern(){
   int activeButton = btnGroup.activeBtnIndex;
   float len = 100;
   len = lengthSlider.sliderVal;
  //use global curPattern
 switch( activeButton ){ ///connects the buttons to the patterns
        //active button sets curPattern 
   case 0: ///eraser button is ButtonArray[0]

        PShape s0 = createShape( ELLIPSE, 0,0,len, len); //this is fine
      //Call constructors to create the objects
       eraserPattern = new Pattern( s0);  //pattern0
       eraserPattern.fillColor = bkgColor;
       eraserPattern.strokeColor = bkgColor;
       curPattern = eraserPattern;
   break;

   case 1:

     PShape s1  = createShape( ELLIPSE, 0,0,len , len/2 );
     pattern1 = new Pattern( s1);
     curPattern = pattern1;
   break;

   case 2:

    PShape s2  = createShape( RECT, 0,0,len , len ); //call vertexShape function

    pattern2 = new Pattern( s2);
        curPattern = pattern2;
   break;

   case 3:

     PShape g = createShape(GROUP);
     recursiveShapes(g,len,5, globalColor); //call vertexShape function

     pattern3 = new Pattern( g);
        curPattern = pattern3;
   break;

   default: 
       //none of the cases were a match
       println("no match on switch-case");
   break;

 } //end of switch
  ////once we know the current pattern, then we are setting the fill and stroke


} //end drawPattern

void displayPattern(){
   if( curPattern != eraserPattern){  //for all other patterns set the stroke and fill
    curPattern.fillColor = color( globalColor);
    curPattern.strokeColor = color(0); //black
     }

  curPattern.display(); //display for every pattern

}

void displayButtons(  ){
  fill( 0);
  rect( 0,0,120, height);
  clearButton.display(); //have the button instance call it's display( ) method
  btnGroup.display(); //ButtonGroup has each button display itself
  particleButton.display();
}

void clearCanvas(){
  ///do something to 'clear the canvas' 

}

PShape vertexShape1( float len, color curColor ) {
  PShape s = createShape( );
  s.setFill(curColor);
  s.beginShape();
  s.vertex(len * .5, len * .5);
  s.vertex( 0, 0);
  s.vertex(len, 0);
  s.vertex( len * .5, len * .5);
  s.vertex( len, len);
  s.vertex(0, len);
  s.vertex( len * .5, len * .5);
  s.endShape(CLOSE);
  return s;
}  //end createOneShape


void recursiveShapes(PShape group,  float len, int level, color c1   ){
  if( level < 1){
    return;
  }
  color curColor = color( hue( c1), saturation(c1), brightness(c1) *.8);
  PShape s = vertexShape1( len, curColor);
  group.addChild(s);
  recursiveShapes( group, len *.8, level-1, curColor);
}
```

