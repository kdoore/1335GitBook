###Project 3 - Main Tab Organization

For Project 3, we'll learn how to create custom classes and then use those classes to create objects in the main tab.

For any objects that will be used in multiple main tab functions such as draw and mouseClicked, then the objects should be declared as globals.

###Declare Global Objects

```java
Button ClearButton;  //example of an object that needs to be global
ButtonGroup buttonGroup;

//declare other global objects
```

###Setup to initialize variables
Use setup to set canvas size and to setup colorMode(HSB), and to initialize all variables

```

void setup(){
    size( 700,700);
    colorMode( HSB, 360, 100, 100);
    
    //initialize objects by calling appropriate constructor
    color defaultBtnColor = color( 280, 100, 100);
    Button ClearButton = new Button( 10, 10, 100, 100, defaultBtnColor, "Clear" ); 

}
```

###Draw function for Displaying Objects



```java

void draw() {

if(mousePressed){
     drawPatterns( );  //all drawing functionality in drawPatterns( ) function
} 

drawMenu( ); //put logic for displaying buttons in drawMenu( ) function
}


```

