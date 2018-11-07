###Drawing Application Logic - 

###Initial Logic

For Project 3, you will create a simple drawing application where 4 buttons allow you to choose which pattern to draw. One additional button will clear the drawing canvas.  3 Sliders will be used to change the hue, saturation, brightness of the pattern that's drawn.

**The code on this page, and the image below shows a first iteration for this project**


![](/assets/Screenshot 2017-03-06 12.05.10.png)

### Overall Project Logic


- Create an array of 4 Buttons that function as a ButtonGroup to control which pattern is drawn.

- Create an additional 5th Button that will clear the canvas, but is not part of the ButtonGroup buttons.

- Create 3 simple patterns (PShapes) that can be drawn at the mouse position, the active pattern can be changed by selecting one of 3 pattern buttons.

- Add logic to have 1 of the 4 pattern buttons work as an eraser ( draw an ellipse with background color)


- Use Functions to organize main-tab Logic
- Use Classes to structure project logic.

## Detailed Project Logic

###Classes:  Button, PImageButton, ButtonGroup, Pattern,  
    
###Global Objects:



```java
  
Pattern pattern0, pattern1, pattern2; //eraser will not use a pattern object

color bkgColor;   //declare global variable
Button myClearBtn; ///simple Button for Clear
ButtonGroup buttonGroup; 

```

    
    
###Logic In Main Tab:  Setup:  

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
        
###Logic In Draw:
- if mousePressed
        - translate(mouseX, mouseY);
        - drawPattern( );
        - resetMatrix();
- drawMenu( ) //always draw menu of Buttons
    
###Logic In MouseClicked:
    
- buttonGroup.clicked( parameters )
- clearButton.click( parameters )
- if clearButton is selected
       - clearCanvas( ) - draw rectangle over the canvas surface
       - reset the clearButton```
 
###Logic in drawPattern:
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
                
          
 ###Logic in clearCanvas:
 
    called when clearBtn has been clicked and has on==true
    
 - set fill
 - draw background-color rectangle to clear the canvas.
 
 ###Logic in drawMenu: 
 
 //5 buttons: 4 buttons in buttonGroup, 1 clearButton
-  draw a menu - background (rectangle)
-  display buttonGroup object
-  display clearButton object 
    
     
 
   
 