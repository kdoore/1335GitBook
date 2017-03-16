# MenuArray Project - Starter Code

MenuArray Class - This code should not be modified by students, but students should understand how the logic of this class and how to use it to create a group of buttons where only one button can be active at a time.

```java
class MenuArray{
    //instance variables
    Button[] btnArray;  //declare an array of Buttons
    int numButtons;     //how many Buttons are there?
    int activeButton=-1;
    
    MenuArray( Button[] _btnArray, int _numButtons){
      this.btnArray=_btnArray;  //initialize instance variables with 
      this.numButtons=_numButtons;
    }
  //methods 
  void display(){
    for(int i=0;i<numButtons;i++){
      btnArray[i].display();
    } //end for
  }// end display
    
   void click(int mx, int my){
     for(int i=0;i<numButtons;i++){
       if(activeButton != i){
        btnArray[i].click(mx, my); //call the click method
        if(btnArray[i].on==true){
          activeButton=i;
          for(int j=0;j<numButtons;j++){
            if(j !=i){
               btnArray[j].on=false;
            } //end if j!=i
          } //end for j
        }//end if on
       }// end if active
    } //end for i
  } // end click
  
}// end class
```
###Button Class 

This is the code for a very simple Button, this class will be used as a base class for creating more specialized buttons types


```java

///this is our Button base-class
class Button{
  //instance variables
  float x, y, w, h;
  boolean on;
  color buttonColorOn, buttonColorOff;

  //default constructor
  Button(){
    this(0,0,50,50); 
  }

  Button( float _x, float _y, float _w, float _h){
      this.x = _x;
      this.y=_y;
      w = _w;
      h = _h;
      on =false;
      buttonColorOn= color(255,0,0);
      buttonColorOff=color(0,255,0);
  }

  //methods
  void display(){
    if(on){
      fill(buttonColorOn);
    }
    else{
      fill(buttonColorOff);
    }
      rect(x,y,w,h);
  }

  void click(int mx, int my){ //check to see if mouse is over button when clicked is called
      if(( (mx > x) && (mx <(x+w)))  && (( my> y  ) && (my < (y+h)))){
          on=!on; 
         // println("buttonState: " + on);
      }//end if
  } // end click

}  //end of Button class

```
###Simple Drawing Application 
Below is code for a simple example of a Drawing Application using the MenuArray to manage a group of Buttons

Main Tab

```java

//Global Variable Declaration

MenuArray myMenuArray;  //this is the only global variable, why is that?

//initialization
void setup(){
  size(400,400);
  int numButtons=3;
  // none of these Buttons or BtnArray are global variables: Why?
  
 Button[] btnArray=new Button[numButtons];
   //   initialize each element
  int size=50;
  btnArray[0] = new Button(50,0 , size,size);
  btnArray[1] = new Button(50,50, size,size);
  btnArray[2] = new Button(50,100, size,size);
  
  myMenuArray = new MenuArray(btnArray, numButtons);
 }                            

void draw(){
  if(mousePressed){
      translate(mouseX, mouseY);
      drawPattern();
      resetMatrix();
  }
  myMenuArray.display();
}

void mouseClicked(){
      myMenuArray.click(mouseX, mouseY);
}

//simple function to connect button logic with drawing simple patterns

void drawPattern(){
    // use a switch case statement instead of nested if/else 
   
   if(myMenuArray.activeButton ==0){
        fill(0); //black
        rect(0,0,50,50);
   }
   else if(myMenuArray.activeButton ==1){
       fill(255);  //white
       ellipse(0,0,50,50);
   }
   else{   //what is the value of myMenuArray.activeButton here?  
        fill(150);  //gray
        ellipse(0,0,50,50);
   }
   

}
```



 

