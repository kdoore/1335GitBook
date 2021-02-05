# Glossary

## noise\( \)

Processing noise\( \) example and comparison with random\( \)

```java

//Noise example, input is a continuously increasing value - like framecount
//noise output is a value between 0.0-1.0, here we multiply it by height to give 
//a value for n that is between 0-height.
//Here, the origin is translated each frame to an x position with value of frameCount
//the y value for the red dot is set by the noise
//the y value for the blue dot is random

void draw() {
  frameRate( 10);
  noStroke();
  if ( frameCount < width) { //only execute while in window
    translate( frameCount, 0);
    float n = noise(frameCount * 0.1) * height;  //get a noisy y value
    fill( 255, 255, 0, 50);
    for ( int i=0; i< height; i+=5) {  //increment i by 5
      ellipse( 0, i, 5, 5); //draw a yellow ellipse at y value of i 
    } //end for
    fill( 255, 0, 0);
    ellipse( 0, n, 8, 8); //noisy y value - red dot
    fill(0, 200, 255);
    float randY = random( 5, height-5); //set y randomly within range of height
    ellipse( 0, randY, 4, 4); //blue dot - random y
  }
}

```

## Finite State Machine

A Finite State Machine \(FSM\) is a formal mathematical model used to represent the dynamic behavior of a system. The system is modeled as an abstract machine that exists in one of a finite number of states. The behavior of the system is well defined. An FSM relies on specification of the list of all possible states and events for the system. For each possible system state,a diagram or table specify the allowable events which cause the system to change to a different state. FSM provides a logical structure to represent an event-driven system, once a system has been specified as an FSM using either a diagram or state-transition table, then writing code to represent the dynamics of system is straightforward.

## Variables

User-defined label which corresponds to a managed memory location to allow storage and retrieval of values that will be changing in a program.

## UML Class Diagram

A graphical representation of the features of a class including: name, variables, methods. Class diagrams can be combined to show relationships between classes such as inheritance and composition relationships. The diagram below shows the Button Class. The PImageButton and PShapeButton classes are child classes, they inherit all of the variables and methods from the Button base class. The only methods that should be specified in the child classes are methods that over-ride the base-class method.

![](../.gitbook/assets/screenshot-2015-10-25-16.59.21.png)

### map\( \)

The Processing [map\( \)](https://processing.org/reference/map_.html) function provides a method to find a value in a given range, given an input value from another range. We can use the map\(\) function to convert a value from it's current range to a target range. If we start with an input hueAngle, and we want to convert it to an 8 bit, 0-255 target range, then we write the function as shown below:

```text
    // map(inputValue, valueStart, valueStop, targetStart, targetStop)
    hueValue= map(hueAngle, 0, 360, 0, 255);
```

### save\( \)

If we want to save our image, we can use the processing save\( \) function and we can call it whenever we press a certain key, like 's'. This will save our image to our sketch folder. The file can be saved in a variety of file formats. [Processing Reference: save\(\)](https://processing.org/reference/save_.html)

```java
void keyPressed(){
  if( key == 's' || key == 'S'){
    save("big.png");
  }
```

