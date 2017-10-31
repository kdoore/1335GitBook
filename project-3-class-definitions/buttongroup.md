#ButtonGroup
The ButtonGroup class manages an array of Button objects, only 1 button can be selected at any time.  The variable: activeButton provides the index of the currently selected Button object.  


###Example Usage

```java

 
//main tab 

Button[] buttons = new Button[3]; //declare button array
   buttons[0] = new Button( btnX, btnY,   buttonSize,buttonSize,colo1 ,color2, "P1");
   buttons[1] = new Button( btnX + 110, btnY, buttonSize,buttonSize,color1 ,color2, "P2");
   ButtonGroup buttonGroup = new ButtonGroup( buttons);
}
   
buttonGroup.display();  //displays each button

buttonGroup.clicked( mouseX, mouseY); //manages button selection logic

```




###Class Definition

```java
class ButtonGroup{
  
  Button[] buttons;
  int activeButton;
  
  ButtonGroup(Button[] buttons){
    this.buttons = buttons;
    activeButton = -1;  //start with none selected
  }
  
  void display(){
    for( int i=0; i< buttons.length; i++){
      buttons[i].display();
    }
  }
  
  int clicked(int mx, int my){
    int selected = -1;
     for( int i=0; i< buttons.length; i++){
        if( buttons[i].selected == false){  //if buttons[i] was not previously selected
             buttons[i].clicked(mx, my); //check to see if it's been clicked
             if( buttons[i].selected == true){  // if it's now selected
                 selected = i;  //set to currently active button
                 activeButton = i;
               for( int j=0; j< buttons.length; j++){  //for all other buttons
                 if( i != j){    
                   buttons[j].reset() ;  //turn the buttons off
                 }
               } 
             }
        }
         
     }  
     return selected;
  }//end clicked method 
  
} // end class ButtonGroup


```

