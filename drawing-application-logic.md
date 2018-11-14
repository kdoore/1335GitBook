###Drawing Application Logic - 

###Initial Logic

For Project 3, you will create a simple drawing application where 4 buttons allow you to choose which pattern to draw. One additional button will clear the drawing canvas.  3 Sliders will be used to change the hue, saturation, brightness of the pattern that's drawn.

**The code on this page, and the image below shows a first iteration for this project**


![](/assets/Screenshot 2017-03-06 12.05.10.png)

## Overall Project Logic - Including Slider Logic

###Button[ ] and ButtonGroup
- Create an array of 4 Buttons that function as a ButtonGroup to control which pattern is drawn.

- Create 4 simple patterns (PShapes) that can be drawn at the mouse position, the active pattern can be changed by selecting one of 4 pattern buttons.

- Add logic to have 1 of the 4 pattern buttons work as an eraser ( draw an ellipse with background color, the eraser color should not be modified by the sliders)

###Individual Button to Clear Canvas
- Create an additional 5th Button that will clear the canvas, but is not part of the ButtonGroup buttons.

###Pattern Objects to draw patterns
- Create 4 Pattern Object instances. 

###CheckSliders( ) must occur before DrawPattern( ) 
- CheckSlider( ) method, checks each slider to see if it's value has changed.  Also includes logic for color dependency between sliders:  
    - satSlider's hue is set by the hueSlider's sliderVal;
    - brightSlider's hue is set by the hueSlider's sliderVal;
    - brightSlider's sat is set by the satSlider's sliderVal;
 
###DrawPattern( ) Switch-case Control Structure
Switch-case structure allows one pattern to be set as active by using the activeBtnIndex of the ButtonGroup, to set an active pattern to be drawn on the canvas.

###Sliders set fillColor for Patterns in DrawPattern( )
   



###Main Tab Create Functions for Structure
- Use Functions to organize main-tab Logic
- Use Classes to structure project logic.

##Detailed Project Logic (no sliders): 

###Declare Global Variables in Main Tab

```java
//Global Variables

Pattern eraserPattern, pattern1, pattern2, pattern3; 

color bkgColor;   //declare global variable
Button myClearBtn; ///simple Button for Clear
ButtonGroup buttonGroup; 

Slider hueSlider, satSlider, brightSlider;

``` 
    
###Logic In Main Tab:  setup( )  

- Set Canvas Size: min: 800 x 600
- Set colorMode - HSB
- **Initialize objects by calling constructors:**

       - **declare an Array of Buttons** 
       
          ```Button[] buttons; ```
       - **initialize Array of Buttons**
       
           `buttons = new Button[4]; `
           
       - **initialize each Array element by calling Button , PImageButton Constructors** 
       _You need to figure out Button constructor parameter values so that buttons are positioned in a vertical stack._
           
    ```java
      color onColor = color(300);  //set custom button colors
      color offColor = color(100);
     buttons[0] = new Button( 20, 20, 100, 100, onColor, offColor,"Eraser" );
 
     //similar parameters for other buttons
     buttons[1] = new PImageButton( parameters ); 
     buttons[2] = new PImageButton( parameters ); 
     buttons[3] = new PImageButton( parameters ); 
            
    ```
   
 - **initialize buttonGroup** by calling ButtonGroup Constructor and pass buttonArray as a parameter
       
      `buttonGroup = new ButtonGroup( buttons);` 
      
  - **initialize clearButton** by calling Button Constructor - use either Button or PImageButton
      
    `clearButton = new Button( parameters );`
    
    - initialize Pattern Objects
        - Create 4 PShapes, pass to Pattern Constructor 
    - Example initialization for 2 Patterns shown below
    - 4 pattern objects required

```java
        PShape EraserPShape = createShape( ELLIPSE, 0,0,30,30);
        EraserPattern = new Pattern( EraserPShape);
    
        PShape shape1 = createShape( RECT, 0,0,30, 80);
        Pattern1 = new Pattern( shape1 );
```  

    - **Initialize Sliders**
       Initialize Sliders by calling constructors with proper input parameters to determine position, size, min, max range
    
    ```java
     hueSlider = new HueSlider( 40, height-100, 200, 50, 0, 360 );
    satSlider = new SatSlider( parameters );
    brightSlider = new BrightSlider(  parameters );
    ```
    
    
    
        
###Logic In draw( ):
- if mousePressed
        - checkSliders( );
        - translate(mouseX, mouseY);
        - drawPattern( );
        - resetMatrix();
- drawButtonMenu( ) //always draw menu of Buttons
 
###Logic in drawPattern( ):
- connects buttons to determine currentPattern
- sets fill for currentPattern using slider's sliderVal
- eraserPattern color is not changed by sliders, should have fillColor, strokeColor set to global bkgColor;
- use switch-case structure
- switch: check which buttonGroup button is active
         
 ```java
 
 void drawPattern( ){
     
     Pattern currentPatttern = eraserPattern;
     
     switch(buttonGroup.activeBtnIndex){
        case 0: 
             currentPattern.setFill(bkgColor);
             currentPattern.setStroke(bkgColor);
             currentPatttern = eraserPattern;
        break;
        
        case 1:
             currentPatttern = pattern1;
        break;
        
        case 2:
             currentPatttern = pattern2;
        break;
        
        case 3:
             currentPatttern = pattern3;
        break;

        default:
              println("no match");
         }//end switch-case
        if( currentPattern != eraserPattern){
            //set color using sliders sliderVal if not the eraserPattern
          float hue = hueSlider.sliderVal;
          float sat = satSlider.sliderVal;
          float bright = brightSlider.sliderVal;
          color currentColor = color( hue, sat, bright);
          
          currentPattern.setFill(currentColor);
        }
        currentPattern.display();
        
    } // end drawPattern();
       ```
                
 
 ###Logic in drawButtonMenu( ): 
 
 Draw 5 buttons: 4 buttons in buttonGroup, 1 clearButton
-  draw a menu-background (rectangle)
-  buttonGroup.display();
-  clearButton.display();
   
 ###Logic In MouseClicked(  ):
    
- buttonGroup.clicked( parameters )
- clearButton.click( parameters )
- if clearButton is selected
       - clearCanvas( ) - draw rectangle over the canvas surface
       - reset the clearButton
      
 #Detailed Logic for Adding Sliders to Drawing Application
    
In this project, sliders will be used to control Hue, Saturation, Brightness of the patterns drawn.  

The sliders must be checked each time the draw-loop executes if the mousePressed, to see if the sliderVal has changed.  

Sliders must always be checked for changes in sliderVal before drawing any patterns.

 `checkSliders( )` is a custom function in the main tab, that contains logic for checking each slider. 
 
 - Declare global variables:  
     `Slider hueSlider, satSlider, brightSlider;`
 - Initialize 3 Sliders in setup( ) by calling child class constructors: example
     `hueSlider = new HueSlider( 40, height-100, 200, 50, 0, 360 );`
 - Incorporate Sliders into project using custom functions:
  - void checkSliders( );
  - void drawSliders ( );
  - in drawPattern( ) - set currentPattern fillColor using sliderVal right before currentPattern is displayed: `currentPattern.display()`
      - see drawPattern above for integration of this example code:

```java
    //Code chunk from drawPattern( ) in main tab
    if( currentPattern != eraserPattern){
    //set color using sliders sliderVal if not the eraserPattern
    float hue = hueSlider.sliderVal;
    float sat = satSlider.sliderVal;
    float bright = brightSlider.sliderVal;
    color currentColor = color( hue, sat, bright);
    currentPattern.setFill(currentColor);
    }
```

###Logic in DrawSliders( )
This code is similar to DrawButtons, we simply want to draw a rectangle behind the sliders, and then have each slider display itself by calling the over-ridden display( ) method.

```java
void drawSliders( ){
  //draw background rectangle behind sliders
  //display hueSlider, example:
  hueSlider.display();
  //display other sliders

}
```
###Logic in CheckSliders( )
In CheckSliders, we must check to see if each slider has been pressed.  We need to set the hue value for the satSlider using the current sliderVal of the hueSlider since the display of satSlider should change when the hueSlider is changed.  Similarly for the brightSlider, it must have it's hue and sat reset to reflect current hueSlider and satSlider values.

```java
void checkSliders(){
  ///update sliders if the mouse has been pressed within their hitbox
  hueSlider.checkPressed( mouseX, mouseY);
  satSlider.hue = hueSlider.sliderVal;
  satSlider.checkPressed( mouseX, mouseY);
  brightSlider.hue = hueSlider.sliderVal;
  brightSlider.sat = satSlider.sliderVal;
  brightSlider.checkPressed( mouseX, mouseY);
}
```

###Additional Logic

# clearButton

 ###Logic in clearCanvas( ):
called when clearBtn has been clicked and has on==true
- set fill
- draw background-color rectangle to clear the canvas.
- reset the button to off (call reset( ) method)