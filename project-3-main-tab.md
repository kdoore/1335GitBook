###Project 3 - Main Tab Organization

###Noun Project
You can use .png or .svg images from the Noun Project.  Please make sure to give credit to the icon designer somewhere in the comments for the main tab of your code
[Noun Project weblink](https://thenounproject.com/)


###Overview of Project 3 Structure - Main Tab Code
For Project 3, we'll learn how to create custom classes and then use those classes to create objects in the main tab.

For any objects that will be used in multiple main tab functions such as draw and mouseClicked, then the objects should be declared as globals.

###Declare Global Objects
Your code might have more or less global objects than listed below.  Several of these objects declared here should actually be local within setup such as: colorList, and patternButtons.


```java

Button clearButton;
Button[] patternButtons;

ButtonGroup buttonGroup;
Pattern pattern1, pattern2, pattern3;

float buttonSize;
color backgroundColor;
color[] colorList;

```

###Setup to initialize variables
Use setup to set canvas size and to setup colorMode(HSB), and to initialize all variables

```

void setup(){
    size( 700,700);
    colorMode( HSB, 360, 100, 100);
   
   //initialize objects by calling appropriate constructor
    
    colorList = new color[3];  //you need 7 colors
    colorList[0] = color(280,100,100); //purple
    colorList[1] = color( 0,0,100);//white
    colorList[2] = color( 0,0,0); //black
    
    //initialize PShapes - use VertexPatterns
    PShape s1 = createShape( ELLIPSE, 0,0,40,40);
    pattern0 = new Pattern(s1, colorList[1] );
    //initialize other patterns

    ClearButton = new Button( 10, 10, 100, 100, colorList[0], "Clear" ); 
    Button[] buttons = new Button[3];  //declare array of Buttons
    buttons[0] = new Button( 120, 10, 100 ,100, colorList[1] ,colorList[2], "Eraser" ); 
    //buttons[1] = PShapeButton( parameter values to match the constructor);
    //buttons[2] = PShapeButton( parameter values to match the constructor);
    //initialize other buttons
    
    buttonGroup = new ButtonGroup(buttons);


   /*initialize remaining objects including colorScheme:
   //where to draw colorScheme along y axis
   float y = height - buttonSize -40; 
   colorScheme = new ColorScheme(colorList, 10,  y , buttonSize  );
   */
   
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
See this page for more detail: [Project 3 - Pattern and Color Logic](/project-3-pattern-and-color-drawing-logic.md)

The drawPattern function should use a switch-case statement to determine which button is active and then set the corresponding pattern to be the curPattern that will be displayed.
curPattern is a local variable in drawPatterns that gets set according to the current active button of the buttonGroup within each switch-case statement.  Since the buttonGroup is initialized to have -1 as the starting value for the activeButton instance variable, we need to keep that in mind when writing the logic to deterime which pattern is initially active.  


```java


void drawPatterns( ){
//logic here to draw patterns

// use switch case structure for button logic to connect 

Pattern curPattern = pattern0; //start with the default pattern - eraser
switch ( buttonGroup.activeButton ){
     case 0:
        curPattern = pattern0;
        break;
        
     case 1:
        curPattern = pattern1;
        break;     
           
   //logic for other cases
     
     default:
        currentPattern = pattern0; //let eraser be default pattern
     break;

} // end of switch-case structure

//set color of pattern here see Project 3 - Pattern and Color Logic page for details

curPattern.display(mouseX, mouseY);   //draw current pattern at mouse position
}//end drawPattern function

```



###drawMenu


```java
void drawMenu( ){
//logic for displaying buttons menu

//draw rectangle behind buttons 

//draw all Button objects
clearButton.display();

// also display buttonGroup, colorScheme
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

    //call clicked for other buttons -
    //call clicked for buttonGroup, colorScheme
}   //end mouseClicked
```

###VertexPattern Functions
At the bottom of the main tab you can put code to draw your vertexPatterns, these functions should be modified so they 
PS
