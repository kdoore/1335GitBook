#ButtonGroup
The ButtonGroup class manages an array of Button objects, only 1 button can be selected at any time.  The variable: activeButton provides the index of the currently selected Button object.  


###Example Usage

```java

 
//main tab 
//create buttons by specifying x, y, w, h and 2 colors for each Button.

Button[] buttons = new Button[3]; //declare button array
   buttons[0] = new Button( 10, 10, 100, 100, color1, color2, "P1");
   buttons[1] = new Button( 10, 120, 100, 100, color1, color2, "P2");
   ButtonGroup buttonGroup = new ButtonGroup( buttons);
}
   
buttonGroup.display();  //displays each button

buttonGroup.clicked( mouseX, mouseY); //manages button selection logic

```

###ButtonGroup Class Definition

```java
//add comments
class ButtonGroup{
  
  //PROPERTIES
  
  Button[] buttons;
  int activeBtnIndex;
  
  //CONSTRUCTORS
  
  //add comments
  ButtonGroup(Button[] buttons){
    this.buttons = buttons;
    activeBtnIndex = 0;  //start with no button selected 
  }
  
  //METHODS
  
  //add comments
  void display(){
    for( int i=0; i< buttons.length; i++){
      buttons[i].display();
    }
  }
  
  //add comments
  boolean clicked(int mx, int my){
    boolean isChanged = false; //has a new button been selected
     for( int i=0; i< buttons.length; i++){
        if( buttons[i].selected == false){  //if buttons[i] was not previously selected
             buttons[i].clicked(mx, my); //check to see if it's been clicked
             if( buttons[i].selected == true){  // if it's now selected
                 isChanged = true;
                 activeBtnIndex = i;
               for( int j=0; j< buttons.length; j++){  //for all other buttons
                 if( i != j){    
                   buttons[j].reset() ;  //turn the buttons off
                 }
               } 
             }
        }
         
     }  
     return isChanged;
  }//end clicked method 
  
} // end class ButtonGroup


```

