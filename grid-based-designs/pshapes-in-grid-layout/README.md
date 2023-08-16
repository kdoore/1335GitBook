# 1D - Array of PShapes for Grid Layout

The first approach for creating grid designs will use a 1-dimensional `Array` of PShape Objects and nested `for-loops` to control x,y positioning of each PShape object. Arrays are a data structure, a structure for storing data. In this case, our 'data' is PShape objects that represent a graphical element we can render on the canvas, for now, we just want to create the PShape objects by setting the vertices and fill properties, we can access the data elements at a later time, to display them on the canvas.

## Declare and Initialize an Array of PShape Objects

The syntax for an array of PShape objects is:

1.  **Declare the array:**&#x20;

    `PShape[ ] myShapes;`
2.  &#x20;**Initialize the array** by specifying the number of elements.

    `myShapes = new PShape[ 10 ];`
3.  &#x20;**Initialize each element in the array**

    `myShapes[ 0 ] = createShape( RECT, 0,0,30,30);`
4.  &#x20;**Remember:** array index values range from( 0 to length-1)

    `myShapes[ 1] //is the second element in the array.`

## Array - Declare and Initialize - Example Code

```java
    void setup(){
       size( 400,400 );   

       PShape[ ] myShapes; //Declare Array
       int rows = 10;
       int cols = 10;
       //we need rows * cols shapes to fill the grid
       int size = width / cols; 
       myShapes = new PShape[ rows * cols ]; //Initialize Array

    }
```

## Initialize the PShape Array Elements

After we initialize the array object, then we need to set each array element so that it contains some valid value. We'll almost always use a for-loop to modify and access each array element.

## Iteration / Repetition

Iteration or Repetition - When working with arrays, we'll often use some type of looping structure so we can do some task with each element of the array. This repetition is also called iteration, and it's a fundamental control-structure used in programming. In the example below,

```java
    //initialize each array element using a for-loop structure

    int numShapes = myShapes.length; //use length property of array.
    for( int i=0; i< numShapes; i++){
        myShapes[i]= createShape( RECT, 0,0,100,100);
    }
```

## Pass Array into Functions

Let's put this logic into a function: Since arrays are objects, when we pass an object into a function we are actually passing the address of the object into the function, so anything done to elements of an array within a function are persisted to the object itself. This is a good thing for us.

```java
void populateShapeList( PShape[ ] shapes, int size) {
  int numShapes = shapes.length; //use length property of array.
  for ( int i=0; i< numShapes; i++) {
    int hueVal = i*3;
    PShape tempShape = vertexPattern1( size, hueVal);
    shapes[ i ] = tempShape;
  } //end for-loop
} //end function

//function to create, and return a single vertex pattern
PShape vertexPattern1( float length, int hue) {
  PShape s = createShape();
  s.beginShape();
  s.fill( hue, 100, 100);
  s.vertex( 0, 0);
  s.vertex( length, 0);
  s.vertex( length, length);
  s.endShape(CLOSE);
  return s;
} //end vertexPattern1
```

## Display our shapes

In the code above, we've just stored a bunch of PShape objects, but we haven't drawn anything to the canvas using the shape( s, x, y) function for PShapes. Our shapes are stored in a 1-Dimensional array, we can think of that as a long vertical list of PShape items, with one PShape item in each row of the list.

## Grid: Nested for-loops

A pair of for-loops will allow us to `iterate` through the array to select each PShape object and set it's xy position for display.

We'll create nested for-loops:

the outer for-loop controls which row is being created \[ i ]

the inner loop creates determines which column \[ j ]

For a single item in the grid, we can refer to that item as having grid coordinates: \[ row: i, column: j ].

## Rows: i,  Columns:  j  and Row-Major Order

The code below shows nested for-loops to change xPos and yPos in a grid pattern, each time the inner loop code is executed, a single shape is displayed: NOTE: In the textbook, Shiffman uses the opposite convention for specifying rows, columns in section 13-9. Processing.org examples use the same syntax as I am using. These 2 approaches are termed - row-major, or column-major ordering. [Row and Column Order, wikipedia ](https://en.wikipedia.org/wiki/Row-\_and\_column-major\_order)

We will follow the convention that the outer for-loop `(i)` is specifying the rows, and the inner for-loop `(j)` specifies the columns in a grid.

**Display a single PShape from our shapes array:**

`shape( shapes[ shapeListIndex ], xPos, yPos);`

## Code to display

```java
void displayShapes( PShape[] shapes, float cellSize, int rows, int cols) {
  //variables to increment position and shapes in for-loop
  float xPos=0; //s coordinate to draw each shape
  float yPos = 0; //y coordinate to draw each shape
  int k = 0; //keep track of current item to draw

  for ( int i= 0; i< rows; i++) { //each row
    for ( int j=0; j< cols; j++) {
      shape(shapes[k], xPos, yPos); //display Shape at xPos, yPos
      k++; //move to the next shape in the array
      xPos += cellSize; //move to next column
    } //end j-loop
    xPos=0; //restart at col 0
    yPos += cellSize; //move yPositions down a row
  } //end i=loop
}// end function
```

![](<../../.gitbook/assets/Screen Shot 2018-09-26 at 7.28.10 AM.png>)

## Complete Code

```java
void setup() {
  size( 400, 400 );
  colorMode(HSB, 360,100,100);
  background(0);
  PShape[ ] myShapes; //Declare Array
  int rows = 10;
  int cols = 10;
  //we need rows * cols shapes to fill the grid
  int size = width / cols;
  myShapes = new PShape[ rows * cols ]; //Initialize Array
  populateShapeList(myShapes, size);
  displayShapes(myShapes, size, rows, cols);
} //end setup

void populateShapeList( PShape[ ] shapes, int size) {
  int numShapes = shapes.length; //use length property of array.
  for ( int i=0; i< numShapes; i++) {
    PShape tempShape = vertexPattern1( size, i*3);
    shapes[ i ] = tempShape;
  } //end for-loop
} //end function

//function to create, and return a single vertex pattern
PShape vertexPattern1( float length, int hue) {
  PShape s = createShape();
  s.beginShape();
  s.fill( hue, 100, 100);
  s.vertex( 0, 0);
  s.vertex( length, 0);
  s.vertex( length, length);
  s.endShape(CLOSE);
  return s;
} //end vertexPattern1

void displayShapes( PShape[] shapes, float cellSize, int rows, int cols) {
  //variables to increment position and shapes in for-loop
  float xPos=0; //s coordinate to draw each shape
  float yPos = 0; //y coordinate to draw each shape
  int k = 0; //keep track of current item to draw

  for ( int i= 0; i< rows; i++) { //each row
    for ( int j=0; j< cols; j++) {
      shape(shapes[k], xPos, yPos); //display Shape at xPos, yPos
      k++; //move to the next shape in the array
      xPos += cellSize; //move to next column
    } //end j-loop
    xPos=0; //restart at col 0
    yPos += cellSize; //move yPositions down a row
  } //end i=loop
}// end function
```
