#Project 3 - Pattern and Color Logic

 In the main tab, we need logic to determine which pattern is active and to set the color for the pattern based on the ColorScheme's active ColorChip and the active pattern Button in the ButtonGroup. This page is focused on the logic in the drawPattern function, it is divided into sections based on the functionality of logic for each task.
 
 Tasks:
 1.  Determine active pattern to be displayed - determined by buttonGroup.activeButton.  We use switch/case structure to connect the patternButtons to the patterns to be drawn.
 2.  Determine active color to be displayed - determined by colorScheme.activeIndex.  We use the activeIndex to access the color[] array of the colorScheme
 3.  Create and set variables for currentPattern and currentColor that are updated based on the buttonGroup.activeButton and colorScheme.activeIndex.
 4. display the currentPattern
 5. make sure logic is designed to handle the initial case when no buttons are selected, make sure the eraserPattern doesn't have it's color changed, it should always be the background pattern.
 
###DrawPattern
In the main tab, the pattern and color logic are to be connected in the drawPatterns function.  drawPatterns() is called within the Processing draw( ) function if the mouse is pressed: 

```java
//declare global variables
Button[] patternButtons;
ButtonGroup buttonGroup;
Pattern eraserPattern, pattern1, pattern2;

//declare other global variables

void setup(){
//other initialization code
 
 
  PShape s0 = createShape( ELLIPSE, 0, 0, 40, 40); //Eraser
  PShape s1 = vertexPattern1( 80); 
  //intialize other shapes
  
  eraserPattern = new Pattern( s0, backgroundColor);  //Eraser
  pattern1 = new Pattern( s1, colorList[1]);
  
  
//initialize other objects
}  //end of setup


void draw() {
  if (mousePressed  ) {
    drawPattern();
  }
    ////display buttons as last code executed in draw()
 drawMenu();
}


void drawPattern() {

  //determine active Pattern
  //determine active Color
  //display currentPattern
  
    }
```

 ###Determine Active Pattern - ButtonGroup
The ButtonGroup object, buttonGroup, manages the pattern Buttons, where the buttonGroup's instance variable: activeButton keeps track of the index of the current active button in the ButtonGroup.  We can use a switch-case to match this activeButton to the pattern represented by the buttonGroup's activeButton.  

1.  Create a local variable:  `Pattern currentPattern`, this gets initialized to refer to the eraserPattern.
2.  Update `currentPattern` in the switch-case statement to refer to whichever pattern button is active:
3.  Display `currentPattern` after color has been set.


```java

void drawPattern() {

//DETERMINE ACTIVE PATTERN

Pattern currentPattern= eraserPattern; 
   switch(buttonGroup.activeButton ){
     
     case 0: 
          currentPattern = eraserPattern;   //eraser
     break;
     
     case 1:
          currentPattern = pattern1;
     break;
     
    ////add other cases
     
     default:
          currentPattern = eraserPattern;  //this is the default situation
     break;  
     
   }

  
  //determine active Color
  //display currentPattern
 }
```

 
 ###Determine Active Color - ColorScheme
 The colorScheme object has an instance variable: activeIndex that refers to the currently active colorChip.  The colorChip displays the color from the colors[] array.  The activeIndex allows us to retrieve the active color from the ColorScheme.  
 
```
int activeIndex = colorScheme.activeIndex;
```

If the activeIndex = -1, then no color has been selected.  In addition, if the current selected pattern is the eraser, then the color must be the backgroundColor instead of the colorScheme's active color.  
 
 1. Create local variable: `color curColor;` 
 2. Initialize to background color if eraserPattern is active or if no colorChip has been selected yet
 3. Otherwise, set curColor using the activeIndex of the colorScheme object to get the corresponding colorChip color.
  
 
 ```java

void drawPattern() {

  //determine active Pattern
  //switch-case statement code
  
  //DETERMINE ACTIVE COLOR
   int activeIndex = colorScheme.activeIndex;
   color curColor = backgroundColor;
   if( activeIndex == -1 || currentPattern == eraserPattern){  //no color has been selected or eraser
     curColor = backgroundColor;
   }
   else{ // use activeIndex to get colorScheme color[]
    curColor = colorScheme.colors[activeIndex];  //find activeColor
  }
  ```java

void drawPattern() {

//determine active Pattern
//switch-case statement code
//DETERMINE ACTIVE COLOR
int activeIndex = colorScheme.activeIndex;
color curColor = backgroundColor;
if( activeIndex == -1 || currentPattern == eraserPattern){ //no color has been selected or eraser
curColor = backgroundColor;
}
else{ // use activeIndex to get colorScheme color[]
curColor = colorScheme.colors[activeIndex]; //find activeColor
}
//currentPattern.strokeColor = backgroundColor; //optional add strokeColor to the pattern class instance variables
currentPattern.shapeColor = curColor;
//display currentPattern
}
```

###Alternate version with more concise code for Color matching logic: 
We can write less code if we use the negated versions of our conditional logic, we can say that if both are true: activeIndex != -1, and currentPattern is not the eraserPattern, then let the color be set by the colorChip buttons.  While negated cases are more concise, sometimes it's easier to understand the logic written with more code as shown above.  The goal is to write code that is easy for you to understand when you return to look at the code 2 years from now.

```java

void drawPattern() {

//determine active Pattern
//switch-case statement code
//DETERMINE ACTIVE COLOR

int activeIndex = colorScheme.activeIndex;
color curColor = backgroundColor;
if( activeIndex != -1 && currentPattern != eraserPattern){   curColor = colorScheme.colors[activeIndex]; //find activeColor
}
currentPattern.shapeColor = curColor;
//display currentPattern
}
```

###Display Current Pattern

Once the logic above has been used, then we can display the current pattern:



```java
void drawPattern(){

  //determine active Pattern
  //switch-case statement code

  //determine active color
  
  //display currentPattern
 
   //currentPattern.strokeColor = backgroundColor; //optional to add strokeColor to the Pattern class and use it in display
   currentPattern.shapeColor = curColor; 
   currentPattern.display(mouseX, mouseY); 

}
```

