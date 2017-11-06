#Project 3 - Pattern and Color Logic

 In the main tab, we need logic to determine which pattern is active and to set the color for the pattern based on the ColorScheme's active ColorChip and the active pattern Button in the ButtonGroup. 
 
###DrawPattern
In the main tab, the pattern and color logic are to be connected in the drawPatterns function.  drawPatterns is called within the Processing draw( ) function if the mouse is pressed: 



```java
//declare global variables
Button[] patternButtons;
ButtonGroup buttonGroup;
Pattern eraserPattern, pattern1, pattern2;

//declare other variables

void setup(){
//other initialization code
 
  PShape s0 = createShape( ELLIPSE, 0, 0, 40, 40); //Eraser
  PShape s1 = createShape( RECT, 0, 0, 40, 40);
  //intialize other shapes
  
  eraserPattern = new Pattern( s0, backgroundColor);  //Eraser
  pattern1 = new Pattern( s1, colorList[1]);
//initialize other patterns
}


void draw() {
  if (mousePressed && mouseY >120 ) {
    drawPattern();
  }
    ////display buttons last in draw()
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

Pattern currentPattern = eraserPattern; 
   switch(buttonGroup.activeButton ){
     
     case 0: 
          currentPattern = eraserPattern;   //eraser
          currentPattern.shapeColor = backgroundColor;
     break;
     
     case 1:
          currentPattern = pattern1;
     break;
     
    ////add other cases
     
     default:
          println("NO match");
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
   color curColor;
   if( activeIndex == -1 || currentPattern == eraserPattern){  //no color has been selected or eraser
     curColor = backgroundColor;
   }
   else{ // use activeIndex to get colorScheme color[]
    //println("curColor " + activeIndex);
    curColor = colorScheme.colors[activeIndex];  //find activeColor
  }
   currentPattern.strokeColor = backgroundColor;
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
 
   currentPattern.strokeColor = backgroundColor;
   currentPattern.shapeColor = curColor; 
   currentPattern.display(mouseX, mouseY); 

}
```

