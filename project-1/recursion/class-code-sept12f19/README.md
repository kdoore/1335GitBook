# Recursion Examples

## Example Class Code

## Intro to Recursion and PShapes

The code below provides an example of a simple recursive function that displays a PShape in a pattern.  In this example, the PShape is created within the recursive function. A more modular approach is to create a recursive function that takes the PShape as an input parameter,  as the repeat structure can be applied to any PShape to create a similar pattern. 

```java
//Recursion and PShapes
  //

  void setup(){
    size( 600, 600);
    colorMode(HSB, 360, 100, 100);
    //drawCircle( width/2, height/2, 500  ); //call shiffman's recursive function
    //PShape myShape1 = createPShape1( 200); //test creating 1 shape
    //shape( myShape1, 200, 200);  //render test shape on canvas
    recursiveMotif( 5, 200); //call custom recursive function
  }
  //create a PShape based on size input parameter
  //return a variable that points to the new PShape object
  PShape createPShape1( float size){
    PShape s = createShape(RECT,0,0,size, size);
    return s;
  }

  //recursive function, takes count and size as input params
  //count controls number of repeats, size used as input to createPShape
  void recursiveMotif( int count, float size ){
    if( count < 1){
      return; //terminate
    }
    //task:  make a shape, render the shape
    PShape myShape1 = createPShape1( size); //call custom shape function
    shape( myShape1, 0,0); //render the shape to canvas

    recursiveMotif( count-1, size * 0.8); //changes in input paramter values control behaviour of recursive call: 

  }

  //Shiffman's recursive circles: Example 8.3
  //https://natureofcode.com/book/chapter-8-fractals/
  void drawCircle( float x, float y, float diameter    ){
    if( diameter < 25){ //termination condition
      return;
    }
   fill( 270, 100, 100);
    //noFill();
    ellipse( x, y, diameter, diameter); //task

    drawCircle( x + diameter/2, y, diameter/2  ); //recursive call
    drawCircle( x - diameter/2, y, diameter/2  ); //recursive call
    drawCircle( x, y + diameter/2, diameter/2  ); //recursive call
    drawCircle( x, y - diameter/2, diameter/2  ); //recursive call

    ellipse( x, y, diameter, diameter); //task
  }
```

