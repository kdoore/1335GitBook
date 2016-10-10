# Abstract Pattern Class

Because we want to have multiple patterns for our drawing application, we need to have a base-class that will allow us to refer to a variety of different pattern class objects to keep track of the current active brush pattern.  The code for most patterns that we would define is simply a display method, without any instance variables. The concept of a default pattern doesn't really make sense, since each of these patterns will be based on a unique class.  The only real shared feature of these Pattern classes is that they will all implement a display method.  Therefore, we can create a base class:  `Pattern` that we define as an `abstract class`.

![](/Screenshot 2016-03-02 06.58.13.png)

1. Any class that inherits from an abstract class must implement any abstract method defined in that class.
2. No object instances can be created from an abstract class, instances can only be created from child-classes of an abstract class. 

```
abstract class Pattern{
  abstract void display();  //must be implemented in child classes
}
```

When creating a child class that inherits from an abstract class, there is no special syntax. However, any child class that inherits from an abstract class must implement the abstract method: void display\(\)

Below is the code for creating a child class: RectanglePattern.  The `extends` keyword is used to indicate that this class is a child-class of the Pattern base class.

```
class RectanglePattern extends Pattern{

  void display(){
    fill(255,0,0);
    rect(mouseX,mouseY,20,20);
  }
}
```

How can we create an instance of a RectanglePattern object in our main tab?

```
// main tab

RectanglePattern myRP;    //declare object reference: 

myRP = new RectanglePattern();  //call default constructor in setup()

myRP.display();  //call the display method in draw()

```

### Abstract Class Instance Variables

In the Pattern class above, there were no instance variables declared.  However, one benefit of inheritance is that child classes inherit all instance variables declared in the base-class.  So, if we want to modify the hue, sat, brightness or other variables in child-classes, we should define those variables in the base class.

![](/Screenshot 2016-03-17 15.17.57.png)

### Abstract Pattern Instance Variables

```
abstract class Pattern{
 float hue, sat, bright,alpha,strokeAlpha, w,h, scale;  // variables we would like to adjust

  ///initialize with some simple defaults
  Pattern(){
    w =10;
    h= 20;
    hue = 200;
    sat=200;
    bright=200;
    alpha=100;
    strokeAlpha = 100;
    scale=1.0;
  }

  abstract void display();

} //end of Pattern class


```

In the main tab, now we can create an instance of the child class patterns to control what pattern is created when a menu button is active.  We can use a baseClass, Pattern, object reference variable to refer to our child class object instances.  We initialize and create our child class instances by calling the default constructors: EraserPattern(), and RectanglesPattern()

```java

MenuArray myMenuArray;
Pattern eraser, rectangles;

void setup() {
  size(600, 600);
  background(255);
  eraser = new EraserPattern();
  rectangles = new RectanglesPattern();
  
   ///code to create buttons and menuArray
   
   } //end setup
   
   void draw(){
      drawPattern();  //put pattern drawing logic in a function
      drawMenu();  //put menu-drawing logic in a funtion
   }

  void drawPattern(){
      switch( myMenuArray.activeButton){
        case -1:
          println("No button selected");
        break;
        
        case 0:
          println("Btn index 0");
          eraser.display();
        break;
        
        case 1:
          println("Btn index 1");
          rectangles.display();
        break;
        
        default;
          println("no button matched");
        break;
      
      } // end switch
  
  
  }// end drawPattern
```

