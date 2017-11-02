#ColorScheme



```
/*
ColorScheme - The object has an array of colorChips, where each represents a color and 
has a selectable Button component.  The constructor takes an array of colors and uses it to 
create an array of colorChips.  
The ColorScheme object has logic to insure that only 1 colorChip is active at any time- 
the activeIndex maintains the index of the currrently selected colorChip.
*/
class ColorScheme{
  
  //PROPERTIES
  
  color[] colors;  //array of colors represented in the scheme
  ColorChip[] colorChips;  //a colorChip object is created for each color in the list
  int  activeIndex = 0;  //start wtih no active color - index keeps track of which ever color is currently selected
  float x, y; //location of the top-left edge of the ColorScheme object
  float size; // size of each each ColorChip - used when creating each colorChip
  
  //CONSTRUCTORS
  
  //Add comments to explain constructor parameters
  ColorScheme(color[] colors, float x, float y, float size){
    this.colors = colors;
    this.x=x;
    this.y=y;
    int xOffset = 3;
    
    // add comments here
    //initialize colorChip array with array of colors
    colorChips = new ColorChip[colors.length]; //initialize array of colorChips, one for each color 
    for( int i=0; i< colors.length; i++){
          colorChips[i] = new ColorChip(x+(size *i)+ xOffset , y , size,size, colors[i], i);
     } 
  }  //end constructor
  
  //METHODS
  
  //add comments - how does display work?
 void display(){
    fill(0);
    rect(0, y-5, width, 200); //background rectangle
    for( int i=0; i< colorChips.length; i++){
      colorChips [i].display();
    }  
  }
  
  
  ///check the button of each ColorChip, see if it's been clicked by the mouse
  //same logic as ButtonGroup
  int clicked(int mx, int my){
    int  selectedIndex = -1;         //return value:  assume nothing has just been clicked, then -1 is returned
     for( int i=0; i< colorChips.length; i++){     //for every colorChip
      if( activeIndex != i){         //if it's not currently active
          colorChips [i].button.clicked(mx, my);      //check and see if mouse within bounding box
         if( colorChips [i].button.selected == true){      //if it's now active, then shut off all other buttons
          activeIndex = i;          //set the activeIndex to the current element - since we now know it's active
          selectedIndex = i;        //update the return value to the currently selected item
           for( int j=0; j< colors.length; j++){       //loop through every colorChip - to turn it off
             if( i != j){           //don't turn off currently selected one, turn off all others
                 colorChips[j].button.reset();
             }
           }
         }
        }
    }
    return selectedIndex;
  }//end function
  
}  //end ColorScheme class
```

