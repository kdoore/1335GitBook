#Arrays of Objects

###Menu Buttons - Radio Group Logic
In the previous section, we discussed how to create a group of buttons which behave like radio buttons.  In our Menu class, we created 3 instances of Button objects, then we defined methods which explicitly called each method for the button object instances.  This is fine for our first pass at creating the Menu class, but once we figured out the required logic for implementing the button behavior, now we need to step back and analyze the code to see if we can make improvements. We can observe that the main function of the Menu class is to implement the Finite State Machine logic to control the activation of the group of Buttons: only 1 button can be active at any time, we need a state variable to remember which button is the currently active button.  

###Observations:
```
    1. Our Menu is not very extensible since we have hard-coded the Button creation logic within 
    the Menu class, we'd prefer flexibility in the number of buttons in our menu.
    
    2. When looking at our code, we observe that we're performing the identical operations on each
    button, this repetition of similar code suggests that using an Array and a loop could simplify
    our code and could provide more flexibility.
    
```
    
###Arrays as Constructor Input Parameters
For maximum flexibility for collections of objects like our Menu that is composed of Buttons, one powerful approach is that we can declare an Array of Buttons as an instance variable for the class, then we can have an Array of Buttons as an input parameter for the Menu Constructor.  This allows us to provide more specific configuration details for each button before adding it to the Menu. 

When we pass an object into any function, what we are actually doing is passing the reference, or memory address, of that object into the function. Since a constructor is a special type of function, objects passed to constructors are also *passed by reference*.  This is extremely helpful for us.  See the section on [Reference Data Types](reference_data_types.md) for more detail on this.   

```java
//Create Class MenuArray 
class MenuArray{
    //instance variables
    Button[] btnArray;  //declare an array of Buttons
    int numButtons;     //how many Buttons are there?
    
    MenuArray( Button _btnArray, int _numButtons){
      btnArray=_btnArray;  //initialize instance variables with 
      numButtons=_numButtons;
    }
  //methods 
}
```
### Use Loops to Iterate through Array Elements
Below is the code in the program's main tab to initialize the btnArray.
```java
//main tab code 

Button[] btnArray; //declare an array of Button objects

MenuArray myMenuArray;

void setup(){
    btnArray=new Button[3];   // initialize array that will hold 3 button
    objects in array positions: btnArray[0], btnArray[1], btnArray[2].
    // use loop to initialize btnArray
    for(int i=0;i < 3; i++){  //Arrays are indexed starting at 0.
        btnArray[i]= new Button(0,(i * 50),50,50);  // for each array element, call the Button constructor, to initialize a Button object.
    }
    myMenuArray = new MenuArray( btnArray, 3);  //call menu constructor using an array input parameter
}
```
If we look at the code for our initial attempt at writing the Menu class, can discover patterns that can help us now that we're trying to modify our code to use an Array of Button objects in our Menu Class.

How can we convert the following code so that it's implemented using an array instead of hard coded Button objects?

```java
void click(int mX, int mY){
        // check to make sure btn1 is not the current activeButton
      if(activeButton != button1){
        btn1.click(mX, mY);   //call the click method for btn1
        if(btn1.on==true){  //the button has just been activated by the click event
            activeButton=button1;  //set to activeButton
            btn2.on=false;  //set btn2 off
            btn3.on=false;  //set btn3 off
         }// end if btn.on
        } // end if activeButton
       //this code must be completed for each of the buttons
      } // end click function
      ```
      
###Array and For-Loop Version
Below is the array version of the above code.  For some sections of the code, psudo-code is used in comments to indicate that additional code needs to be added to implement the specified functionality.  

Can you complete the code below, given the hints telling the logic that needs to be implemented?

```java

void click(int mX, int mY){
    for(int i=0;i< numButtons; i++){//outer loop through each button
            // check to make sure btn1 is not the current activeButton
    if(activeButton != btnArray[i]{
        btnArray[i].click(mX, mY)//call the click method for btn1
        if(btnArray[i].on){  //check to see if btn has been turned on
           activeButton=btnArray[i];  //set activeButton
                    //shut all other buttons off
           for( var j=0;j <numButtons; j++){
                    //for all buttons that aren't i==j
                    //turn button to off state
           }
        }
    } //end if activeButton  
    }// end outer for-loop
}//end click function

```
