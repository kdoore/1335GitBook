# Buttons as Objects

## Buttons as Objects

In the previous sections, we discussed buttons in terms of features

## Physical Objects

When we use a physical button, like the on-off button of a light-switch, we understand that the button has a physical configuration that controls electrical current to the bulb. The physical movement of the switch itself is responsible for controlling the state of the lightbulb as well as controlling the state of the switch itself, so we can look at the switch and understand if it's in the on or off position. However, when we think about a virtual button on a device such as our mobile phone, there is not a tangible, physical configuration of the button that controls these behaviors. To be intuitive for a user, the virtual button should behave analogously to the physical version, so it is helpful for us to think of buttons that we create as if they were physical objects.

## Object Responsibilities

If we think of our button as a physical object, then it makes sense for our button object to be responsible for it's own behaviors and states. A physical button has a configuration that controls and indicates if it's on or off. For our button, we need to create a _state variable_, **`selected,`** so the button object can remember whether it is currently on or off. Similarly, we want the button to be responsible for responding to user-events, and it's display (behavior), and for knowing it's current state, size, position and orientation (state and configuration). Then we can have many button instances, each responsible for is own object properties, and the object behaviors (methods) will be consistent across all instances.

## Objects and Classes

To create objects, we write code to define a **class**, which we can think of as the **blueprint** for creating objects. When creating objects in code, it's helpful to think of object responsibilities in terms of what information an object knows about itself, and the behaviors an object can do. In our code, we will use **instance variables** to store an object's state and configuration information. To implement an object's behaviors, we'll write functions, these are referred to as the object's **methods**. Once we write code to define the Button class, then we can create an unlimited number of button objects. When our code is executed, then the button objects are created where the compiler uses the class code as the blueprint.

## Object - Class Structure

The image below is a **UML Class Diagram**. [UML](http://www.omg.org/gettingstarted/what\_is\_uml.htm) _Unified Modeling Language_ is modeling language specification that provides formal structures for designing models of systems. The [UML](http://www.omg.org/gettingstarted/what\_is\_uml.htm) website states that 'modeling is the designing of software applications before coding.'

![](<../../.gitbook/assets/Screen Shot 2019-04-01 at 7.45.41 AM.png>)

The class diagram shows the name of the class, the instance variables, and the methods. In UML, we can use class diagrams to show relationships between several different classes. There are a wide variety of UML diagrams, some are designed to show structure like this class diagram, while other UML diagrams are designed to model behavior and interaction of system entities.

## Processing Tabs

Processing provides tabs to allow us to organize our code when using classes, the main tab is the name of the sketch, while each other tab should be the name of the class, such as Button. The image below shows the Button tab with the basic code elements which define the class.

![](<../../.gitbook/assets/Screen Shot 2019-04-01 at 7.49.44 AM.png>)

When looking at the code in a Class definition, we can see a similarity with the structure of code that we've been writing in our previous examples. The table below shows these similarities, in the left column, we can see that the code we write in the main tab can be though of as having 3 sections, the top of our programs is where we declare global variables, then the setup() function is executed once, while the draw() function is where the main behavior of our program is typically executed. When we write code for a class definition, we are required to write our instance variables at the top, then we must write the constructor functions, these are similar to setup() in that the constructor for an object is a function that is only executed once, when the object is first created and it's used to initialize all of the instance variables for our object. Finally, the bottom of the tab contains all of the functions / methods that we write for our object's behaviors. Within these methods, we can also have local variables, but they will only exist for the duration of that method's execution. The instance variables exist for the life of the object instance, store all of the information about the state and configuration of our object instances throughout the duration of an object's lifetime.

### Button Class Definition

```java
class Button{
  ////Instance Variables - Properties
  float x, y;   //position
  float w, h;   //size dimensions
  boolean selected;
  color defaultColor, selectedColor, currentColor;
  String label;  ///text to display

  /////Constructor Methods
  /////Initialize our instance variables
  ////Overloaded versions of constructors - unique parameter lists

  Button( float _x, float y, float w, float h, color onColor, color offColor, String label){
    x = _x;   //set value for class variable x, using parameter _x
    this.y = y;
    this.w = w; 
    this.h = h;
    selectedColor = onColor;
    defaultColor = offColor;
    currentColor = defaultColor;  ///button is off to begin with, so use default color 
    selected = false;
    this.label = label;
  }

////Class Methods
  void display(){
    fill(currentColor);
    rect( x, y, w, h);
    fill(0); //black
    textAlign(CENTER);
    textSize(20);
    text(label, x + w/2, y + h/2);  //display label
  }

  void clicked(int mx, int my){
    if( mx > x && mx < x+w && my >y && my < y+h){   //button has been clicked
      if( selected == true){
        selected = false;
        currentColor = defaultColor;
      }else{      //had been selected == false
         selected = true;
         currentColor = selectedColor;
      } //end else
    }  //end outer if
  } ///end of clicked

    //sets the button to off state
    void reset(){
       selected = false;
       currentColor = defaultColor;
    }


}  ///end of the Button Class
```

![](../../.gitbook/assets/MainVsClass.png)

In [Shiffman's book](http://learningprocessing.org),he provides example code for how to make an Button class as part of his example problems: 9.8.

### Main Tab - Creating Button Objects

The code below is from the main tab for a simple program which uses the Button class to make Button objects. The code shows the comparison between how to declare and initialize primitive variables like int. When creating objects, it's necessary to call the class constructor function.

### Clear Button

The example code below also creates a clear button. In the draw loop, we check to see if the myClearBtn.on is true, if it is, then we draw a large rectangle that is the size of the canvas. Then we must remember to set the state to on=false.

```java
//initialization
Button button1; //we declare the type: Button, then the name: myButton
Button button2;
Button myClearBtn;

void setup(){
  size(400,400);
  colorMode( HSB, 360, 100,100);
  color colorOn = color(250, 50, 100);//purple
  color colorOff = color(250, 50, 50);//dark purple

  button1 = new Button(30,30,100,100, colorOn, colorOff, "Btn1" );  //create object-instance using 'new' keyword, call a constructor
  button2 = new Button(30,130,100,100, colorOn, colorOff, "Btn2" );  //create object-instance using 'new' keyword, call a constructor
  myClearBtn = new Button(30,230,100,100, colorOn, colorOff, "Clear" );  //create object-instance using 'new' keyword, call a constructor
}                            

void draw(){
  background(255);
  button1.display();   //we use 'dot-notation' to call the Button Display() method
  button2.display();
  myClearBtn.display();
}

//check to see if each button has been clicked
void mouseClicked(){
  button1.clicked(mouseX, mouseY); 
  button2.clicked(mouseX, mouseY);
  myClearBtn.clicked(mouseX, mouseY);

  //add logic to clear the screen
  if(myClearBtn.selected == true){  //see if the clear button has been clicked
    clearScreen();
    myClearBtn.reset();   //turn the button off!
  }
}

void clearScreen(){
  fill(255);
  rect(0,0,width, height);
}
```

### Questions

1. What is the difference between a class and an object?
2. What is the difference between a constructor and a method?
3. What is a default constructor?
4. What is an object instance?
5. What does a constructor do?
6. How do we execute a method for an object instance?
