###Drawing Application Logic - 

###Initial Logic

For Project 3, you will create a simple drawing application where 3 buttons allow you to choose which pattern to draw. One additional button will clear the drawing canvas.  

**The code on this page, and the image below shows a first iteration for this project**


![](/assets/Screenshot 2017-03-06 12.05.10.png)

### Overall Project Logic


- Create a Group of 3 Buttons that function as a group

- Create a single Button to clear the canvas

- Create 3 simple patterns that can be drawn at the mouse position, the active pattern can be changed by selecting one of 3 buttons

- Use Functions to organize main-tab Logic
- Use Classes to structure project logic.

## Detailed Project Logic

###Classes:  Button, ButtonGroup, Pattern
    
###Global Objects:



```java
  
Pattern pattern0, pattern1, eraserPattern;

color bkgColor;   //declare global variable
Button myClearBtn; ///simple Button for Clear
ButtonGroup buttonGroup; 

```

    
    
###Logic In Setup:  

- Set Canvas Size
- Set colorMode - HSB
- Initialize objects by calling constructors:
       - declare an Array of Buttons //local to setup
       
          ```Button[] btnArray; ```
       - initialize Array of Buttons
       
           `btnArray = new Button[3]; `
       - initialize each Array element by calling Button Constructor
           
            btnArray[0] = new Button( parameters ); 
       - initialize clearButton by calling Button Constructor
       
       clearButton = new Button( parameters ); 
       
       - initialize buttonGroup by calling ButtonGroup Constructor and pass buttonArray as a parameter
       
      buttonGroup = new ButtonGroup( btnArray); 
    
###Logic In Draw:
- if mousePressed
        - drawPattern
- drawMenu //always draw menu of Buttons
    
###Logic In MouseClicked:
    
- buttonGroup.click
- clearButton.click
- if clearButton is on ```if(clearButton.on)```
       - clearCanvas - draw rectangle over the canvas surface
       - reset the clearButton```
 
###Logic in drawPattern:
- translate origin to mouse position
- set fill color
- use switch-case structure
- switch: check which myMenuArray button is active
         
         ```java
         
         switch(buttonGroup.activeButton){
         case 0:
             //display pattern 0
             break;
          case 1:
             //display pattern 1
             break;
          case 2:
             //display pattern 2
             break;
          default:
              //println - no match
            break;
            }
       ```
       
- resetMatrix
          
          
 ###Logic in clearCanvas:
 
    called when clearBtn has been clicked and has on==true
    
 - set fill
 - draw background-color rectangle to clear the canvas.
 
 ###Logic in drawMenu: 
 
 //4 buttons - 3 patterns, 1 clearButton
-  draw a menu - background (rectangle)
-  display buttonGroup object
-  display clearButton object 
    
     
 
   
 