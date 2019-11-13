##Class Code - Nov. 13,2019


```java
///Main tab
Button  clearBtn; //null    declare the obj ref variable 
ButtonGroup buttonGroup; //global
color backgroundColor;
Slider scaleSlider, hueSlider, satSlider, brightSlider;
Pattern eraserPattern, pattern1, pattern2, pattern3;

void setup(){
  size( 1000, 800);
  colorMode( HSB, 360, 100, 100);
  backgroundColor = color( 50);
  background(backgroundColor); //set background one time
  
  PImage img = loadImage("pattern1Btn.png");
  //image( img, 300, 50, 50, 50);  //SEE the image displayed - check for errors
  
  clearBtn = new Button( 10,10,100,100, "Clear"); //same size, located below
  
  Button[] btnArray = new Button[4]; 
  //Button ( float x, float y, float w, float h, String label)
  
  //initialize each Button in the btnArray to pass to ButtonGroup
  btnArray[0] = new Button(10,120, 100, 100,"Eraser");
  btnArray[1] = new PImageButton( 10, 230, 100, 100, img);
  btnArray[2] = new Button( 10, 340, 100, 100, "Btn2");
  btnArray[3] = new Button( 10, 450, 100, 100, "Btn3");
  buttonGroup = new ButtonGroup( btnArray);
  
  //Slider(float x, float y, float w, float h, float min, float max, String label ){
  
  scaleSlider = new Slider(30, height - 100, 100, 50, 0.2, 2.0, "Scale");
  hueSlider = new HueSlider(  160,height-100,200,50,0, 360 );
  satSlider = new SatSlider(  400,height-100,200,50,0, 100 ); //saturation 0-100
  satSlider.hue = hueSlider.sliderVal;
  
  PShape s0 = createShape(ELLIPSE, 0,0,50,50);
  eraserPattern = new Pattern( s0 ); //pass in an PShape
  PShape s1 = createShape( RECT, 0,0, 60, 40);
  pattern1 = new Pattern( s1);
  PShape s2 = createShape( ELLIPSE, 0,0, 50, 20);//oval
  pattern2 = new Pattern(s2);
  PShape s3 = createShape( RECT, 0,0,50,50);//square
  pattern3 = new Pattern(s3);
 }

void draw(){
  if( mousePressed){
    checkSliders();
    
    pushMatrix();
    translate( mouseX, mouseY);
    scale( scaleSlider.sliderVal); //use the slider's sliderVal to set the scale 
    drawPattern();
    popMatrix();
  }
  drawBtnMenu();
  drawSliderMenu();
} //end Draw()

void mouseClicked(){
  //have the buttonGroup check if any button has been clicked
   buttonGroup.clicked( mouseX, mouseY);
if( clearBtn.clicked( mouseX, mouseY)){
    clearCanvas();
    clearBtn.reset(); //turn off - right after use - like a doorbell
  }
} //end mouseClicked

//Check if any sliders have been changed
//Have logic for dependancy between sliders:  - a bit of a hack - 
void checkSliders(){
  scaleSlider.checkPressed( mouseX, mouseY);
  if(hueSlider.checkPressed( mouseX, mouseY)){ //call base-class method
     //we know the hueSlider has changed
     satSlider.hue = hueSlider.sliderVal; ////dependency satSlider's hue changes if hueSlider changes
     //brightSlider.hue = hueSlider.sliderVal; ////depepndency: brightSlider's hue changes when hueSlider changes
    }
  if(satSlider.checkPressed( mouseX, mouseY)){
    //brightSlider.sat = satSlider.sliderVal; ///dependency:  brightSlider's sat changes when satSlider changes
  }
  
}


void drawSliderMenu(){
  fill(0); //black
  rect( 0,height-150, width, 150); //background rectangle for menu
  scaleSlider.display();
  hueSlider.display(); //call over-ride method in child class
  satSlider.display(); //call over-ride method in the child class
  //add code to display brightSlider
}


void clearCanvas(){
    fill(backgroundColor);
    rect( 0,0, width, height);
} //end clearCanvas

void drawBtnMenu(){
  fill(0); //black background 
  rect( 0,0,120, height);
  buttonGroup.display();
  clearBtn.display();
} //end drawBtnMenu

//FMS- ButtonGroup FSM
//connect buttonGroup with our patterns 
void drawPattern(){
 
  Pattern curPattern = eraserPattern;  //temp variable to hold current Pattern
  
  switch( buttonGroup.activeBtnIndex){
    case 0:
      //eraser - special case
     curPattern = eraserPattern;
     curPattern.fillColor = color( backgroundColor);
     curPattern.strokeColor = color(backgroundColor);
    break;
    
    case 1: //buttonGroup with index 1
      curPattern = pattern1;
    break;
    
    case 2:
       curPattern = pattern2;
    break;
    
    case 3:
      curPattern = pattern3;
    break;
    
    default:
       println("No match on switch value");
  } //end switch statement
  if( curPattern != eraserPattern){
    //set color using sliders - if not eraser
    float hue = hueSlider.sliderVal;
    float sat = satSlider.sliderVal;
    float bright = 100;  //you will change this once you have a bright slider
    curPattern.fillColor= color( hue, sat, bright); //update the color using sliders
    curPattern.strokeColor = color(0);//black
    }
  curPattern.display();  //whatever the pattern is, display it
} //end drawPattern()
```

