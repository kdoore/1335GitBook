###Drawing Application Logic

For Project 2, you will create a simple drawing application where 3 buttons allow you to choose which pattern to draw. One additional button will clear the drawing canvas.  The image below shows a first iteration for this project

![](/assets/Screenshot 2017-03-06 12.05.10.png)

### Overall Project Logic


Create a Group of 3 Buttons that function as a group

Create a single Button to clear the canvas

Create 3 simple patterns that can be drawn at the mouse position, the active pattern can be changed by selecting one of 3 buttons

Use Functions to organize main-tab Logic
Use Classes to structure project logic.

### Detailed Project Logic
Classes:  Button, MenuArray
    
Global Objects:

    MenuArray myMenuArray
    Button clearButton
    
In Setup:  

    - Set Canvas Size
    - Set colorMode - HSB
    - Initialize objects by calling constructors:
       - declare Array of Buttons 
       
          ```Button[] btnArray;``` 
       - initialize Array of Buttons
       
           ```btnArray = new Button[3];```
       - initialize each Array element by calling Button Constructor
           
           ```myMenuArray[0] = new Button( parameters );```
       - initialize clearButton by calling Button Constructor
       
       ```clearButton = new Button( parameters );```
       
       - initialize myMenuArray by calling MenuArray Constructor and pass buttonArray as a parameter
       
     ```myMenuArray = new MenuArray( btnArray, 3);```
    
Logic In Draw:
    - if MousePressed
        - drawPattern
    - drawMenu
    
Logic In MouseClicked:
    
    - myMenuArray.click
    - clearButton.click
    - if clearButton is on
       - clearCanvas
       - turn off clearButton
 
 
 Logic in drawPattern:
 
 Logic in clearCanvas:
 
 Logic in drawMenu:
     -  draw background rectangle
     -  display menuArray object
     -  display clearButton object 
    
    
 Functions:  
 