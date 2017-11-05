###Project 3 - Main Tab Organization

###Noun Project
You can use .png or .svg images from the Noun Project.  Please make sure to give credit to the icon designer somewhere in the comments for the main tab of your code
[Noun Project weblink](https://thenounproject.com/)


###Overview of Project 3 Structure - Main Tab Code
For Project 3, we'll learn how to create custom classes and then use those classes to create objects in the main tab.

For any objects that will be used in multiple main tab functions such as draw and mouseClicked, then the objects should be declared as globals.

###Declare Global Objects

```java
Button ClearButton;  //example of an object that needs to be global
ButtonGroup buttonGroup;
Pattern pattern0, pattern1, pattern2
//declare other global objects like colors array, colorScheme object
```

###Setup to initialize variables
Use setup to set canvas size and to setup colorMode(HSB), and to initialize all variables

```

void setup(){
    size( 700,700);
    colorMode( HSB, 360, 100, 100);
    
    //initialize objects by calling appropriate constructor
    color defaultBtnColor = color( 280, 100, 100);
    ClearButton = new Button( 10, 10, 100, 100, defaultBtnColor, "Clear" ); 

}
```

###Draw function for Displaying Objects
Within the draw function, use functions call logical modules 


```java

void draw() {

if(mousePressed){
     drawPatterns( );  //all drawing functionality in drawPatterns( ) function
} 

drawMenu( ); //put logic for displaying buttons in drawMenu( ) function
}


```

###Modular Functions for Main Tab Logic
###drawPatterns function 
The drawPattern function should use a switch-case statement to determine which button is active and then set the corresponding pattern to be the curPattern that will be displayed.
curPattern is a local variable in drawPatterns that gets set according to the current active button of the buttonGroup within each switch-case statement.  Since the buttonGroup is initialized to have -1 as the starting value for the activeButton instance variable, we need to keep that in mind when writing the logic to deterime which pattern is initially active.  


```java


void drawPatterns( ){
//logic here to draw patterns

// use switch case structure for button logic


Pattern curPattern = pattern0; //start with the default pattern - eraser
switch ( buttonGroup.activeButton ){
     case 0:
        curPattern = pattern0;
        break;
        
        
   //logic for other cases
     default:
        println("no pattern selected");
     break;

} // end of switch-case structure

//set color of pattern here

curPattern.display(mouseX, mouseY);   //draw current pattern at mouse position
}//end drawPattern function

```



###drawMenu


```java
void drawMenu( ){
//logic for upper menu

//draw rectangle behind buttons 

//draw all Button objects
clearButton.display();

}

```



###MouseClicked Function

```java
void mouseClicked( ){
 
 clearButton.clicked( mouseX, mouseY );
 if(clearButton.selected){
     //draw big rectangle to clear screen
     //reset clearButton.
 }
 
 //call .clicked for other buttons
}  //end mouseClicked
```

