# ButtonGroup - Final Version

## Button Group - Radio Group Logic

In the previous section, we discussed how to create a group of buttons which behave like radio buttons. In our ButtonGroup class, we created 3 instances of Button objects, then we defined methods which explicitly called each method for the button object instances. This is fine for our first pass at creating the Menu class, but once we figured out the required logic for implementing the button behavior, now we need to step back and analyze the code to see if we can make improvements. We can observe that the main function of the Menu class is to implement the Finite State Machine logic to control the activation of the group of Buttons: only 1 button can be active at any time, we need a state variable to remember which button is the currently active button.

## Observations: Version 1: Menu of Buttons

1. Our first version for the Menu of Buttons is not very extensible since we have hard-coded the Button creation logic within the ButtonGroup class, we'd prefer flexibility in the number of buttons in our menu.
2. When looking at our code, we observe that we're performing the identical operations on each button, this repetition of similar code suggests that using an Array and a loop could simplify our code and could provide more flexibility.

## Arrays as Constructor Input Parameters

For maximum flexibility for collections of objects like our ButtonGroup that is composed of Buttons, one powerful approach is that we can declare an Array of Buttons as an instance variable for the class, then we can have an Array of Buttons as an input parameter for the ButtonGroup Constructor. This allows us to provide more specific configuration details for each button before adding it to the ButtonGroup.

When we pass an object into any function, what we are actually doing is passing the reference, or memory address, of that object into the function. Since a constructor is a special type of function, objects passed to constructors are also _passed by reference_. This is extremely helpful for us. See the section on [Object Reference Data Types](https://github.com/kdoore/cs1335-java-and-processing/tree/9e8e8ed05c8db5e0695fd2711a01f24b372e8118/reference_data_types.md) for more detail on this.

```java
//Create Class ButtonGroup
class ButtonGroup{
    //instance variables
    Button[] buttons;  //declare an array of Buttons
    int numButtons;    //how many Buttons are there?
    int activeBtnIndex; //currently selected Button (FSM memory)

    ButtonGroup( Button buttons){ //constructor method
      this.buttons =buttons;  //initialize instance variables with 
      numButtons=buttons.length;
      activeBtnIndex=0; //set default
    }
  //methods 
}
```

## Initialize Button Array in Main Tab

Below is the code in the program's main tab to initialize the `buttons` array.

```java
//main tab code 

Button[] btnArray; //declare an array of Button objects

ButtonGroup myBtnGroup;

void setup(){
    color c1 = color(100);
    color c2 = color(250);

    btnArray=new Button[3];   // initialize array that will hold 3 button
    btnArray[0]= new Button(0,0,50,50,c1, c2, "Btn1" );  // for 
    btnArray[1]= new Button(0,50,50,50,c1, c2, "Btn2"); 
    btnArray[2]= new Button(0,100,50,50,c1, c2, "Btn3"); each array element, call the Button constructor, to initialize a Button object.

    myBtnGroup = new ButtonGroup( btnArray);  //call menu constructor using an array input parameter
}
```

If we look at the code for our initial attempt at writing the [ButtonGroup class](https://github.com/kdoore/cs1335-java-and-processing/tree/9e8e8ed05c8db5e0695fd2711a01f24b372e8118/menu_buttons.md), can discover patterns that can help us now that we're trying to modify our code to use an Array of Button objects in our Menu Class.

## ButtonGroup clicked\(int mx, int my\)

Below is the array version of the above code. See comments to indicate that additional code was added to implement the specified functionality.

```java
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
```

### Final Version of Button Group

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

