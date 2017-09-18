#PShape Objects in a Grid Layout

The first approach for creating grid designs will use an ``Array`` of PShape Objects and nested ``for-loops`` to control x,y positioning of each PShape object.

###Declare and Initialize an Array of PShape Objects

The syntax to create an array of PShape objects is: 
    1. Declare the array:  ``PShape[ ] myShapes``;
    2. In setup:  initialize the array by specifying the number of elements.
    

```java
  
    void setup(){
       size( 400,400);
       
       PShape[ ] myShapes; //Declare Array
       int rows = 10;
       int cols = 10;
       //we need rows * cols shapes to fill the grid
       int size = width / cols; 
       myShapes = new PShape[ rows * cols ]; //Initialize Array
     
    }
```
  
    
 ###Initialize the PShape Array Elements
  
 After we initialize the array object, then we need to set each array element so that it contains some valid value.  We'll almost always use a for-loop to modify and access each array element.
    
    
    ```java
    int numShapes = myShapes.length; //use length property of array.
    for( int i=0; i< numShapes; i++){
    PShape tempShape = createShape(ELLIPSE, 0,0,cellSize-10,cellSize-5);
         _shapes[ i ] = tempShape;  
        }
 
```    

###Pass Array into Functions
Let's put this logic into a function:
Since arrays are objects, when we pass an object into a function we are actually passing the address of the object into the function, so anything done to elements of an array within a function are persisted to the object itself.  This is a good thing for us.

```java
//function to put a PShape object in each array element 
//shapes: PShape array
//size: dimensions for each PShape design

void populateShapeList( PShape[ ] shapes, int size){
    int numShapes = shapes.length; //use length property of array.
   for( int i=0; i< numShapes; i++){
        PShape tempShape = createShape(ELLIPSE,    0,0,size,size);

        _shapes[ i ] = tempShape 
    } //end for-loop
} //end function

```

###Display our shapes
In the code above, we've just stored a bunch of PShape objects, but we haven't drawn anything to the canvas using the shape( s, x, y) function for pshapes.  

A set of for-loops will allow us to ``iterate`` through the array to select each PShape object and set it's xy position for display.

###Rows: i,  Columns:  j


 ```java
 
void displayShapes( PShape shapes){
  float xPos=0;  //s coordinate to draw each shape

  float yPos = 0;  //y coordinate to draw each shape
  int curIndex = 0;  //keep track of current item to draw
  float size = width / rows;  //each grid's size

  for( int i= 0; i< rows; i++){ //each row
    for( int j=0; j< cols; j++){
       shape(shapes[curIndex], xPos,yPos);  //display Shape at xPos, yPos
       curIndex++;
       xPos+= size; //move to next column
     }  //end j-loop
  xPos=0; //restart at col 0
  yPos += size; //move yPositions down a row 
  } //end i=loop 
 
 }// end function


```




