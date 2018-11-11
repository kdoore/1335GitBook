###Drawing Application Logic - 

###Initial Logic

For Project 3, you will create a simple drawing application where 4 buttons allow you to choose which pattern to draw. One additional button will clear the drawing canvas.  3 Sliders will be used to change the hue, saturation, brightness of the pattern that's drawn.

**The code on this page, and the image below shows a first iteration for this project**


![](/assets/Screenshot 2017-03-06 12.05.10.png)

# Overall Project Logic - Phase 1

###Button[ ] and ButtonGroup
- Create an array of 4 Buttons that function as a ButtonGroup to control which pattern is drawn.

- Create 4 simple patterns (PShapes) that can be drawn at the mouse position, the active pattern can be changed by selecting one of 4 pattern buttons.

- Add logic to have 1 of the 4 pattern buttons work as an eraser ( draw an ellipse with background color, the eraser color should not be modified by the sliders)

###Individual Button to Clear Canvas
- Create an additional 5th Button that will clear the canvas, but is not part of the ButtonGroup buttons.

###Pattern Objects to draw patterns
- Create 4 Pattern Object instances. 
 
###Switch-case Control Structure
Switch-case structure allows one pattern to be set as active by using the activeBtnIndex of the ButtonGroup, to set an active pattern to be drawn on the canvas.

###Main Tab Create Functions for Structure
- Use Functions to organize main-tab Logic
- Use Classes to structure project logic.

# Detailed Project Logic - Part 1 (no sliders): 

###Declare Global Variables in Main Tab

```java
//Global Variables

Pattern eraserPattern, pattern1, pattern2, pattern3; 

color bkgColor;   //declare global variable
Button myClearBtn; ///simple Button for Clear
ButtonGroup buttonGroup; 

``` 
    
###Logic In Main Tab:  setup( )  

- Set Canvas Size: min: 800 x 600
- Set colorMode - HSB
- **Initialize objects by calling constructors:**

       - **declare an Array of Buttons** 
       
          ```Button[] buttons; ```
       - **initialize Array of Buttons**
       
           `buttons = new Button[4]; `
       - **initialize each Array element by calling Button Constructor**
           
    ```java
     buttons[0] = new Button( parameters, "Eraser" ); 
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
        
###Logic In draw( ):
- if mousePressed
        - translate(mouseX, mouseY);
        - drawPattern( );
        - resetMatrix();
- drawButtonMenu( ) //always draw menu of Buttons
 
###Logic in drawPattern( ):
- set fill color
- use switch-case structure
- switch: check which myMenuArray button is active
         
         ```java
         
         switch(buttonGroup.activeBtnIndex){
         case 0:
             //display pattern 0
             break;
          case 1:
             //display pattern 1
             break;
          case 2:
             //display pattern 2
             break;
          case 3:
             //display pattern 2
             break;

          default:
              //println - no match
            break;
            }
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
   
      
  ###Logic in clearCanvas( ):
 
    called when clearBtn has been clicked and has on==true
    
 - set fill
 - draw background-color rectangle to clear the canvas.
   
 #Detailed Logic for Adding Sliders to Drawing Application
 
 //todo
   
 