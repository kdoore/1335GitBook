#PShape Objects in a Grid Layout

The first approach for creating grid designs will use a 1-dimensional ``Array`` of PShape Objects and nested ``for-loops`` to control x,y positioning of each PShape object.
Arrays are a data structure, a structure for storing data.  In this case, our 'data' is PShape objects that represent a graphical element we can render on the canvas, for now, we just want to create the PShape objects by setting the vertices and fill properties, we can access the data elements at a later time, to display them on the canvas.

###Declare and Initialize an Array of PShape Objects

The syntax for an array of PShape objects is:
 
  1. **Declare the array: ** 
  
   ` PShape[ ] myShapes;`
 
  2. ** Initialize the array** by specifying the number of elements. 
  
    `myShapes = new PShape[ 10 ];`
    
  3. ** Initialize each element in the array**
  
    `myShapes[ 0 ] = createShape( RECT, 0,0,30,30);`
    
  4. ** Remember: ** array index values range from( 0 to length-1)  
  
    `myShapes[ 1] //is the second element in the array.`
    
    
###Array - Declare and Initialize - Example Code

  ```java
  
    void setup(){
       size( 400,400, P2D);  //if you can use P2D otherwise size( 400,400);
       
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

###Iteration
Iteration 
    
    
```java
    
    int numShapes = myShapes.length; //use length property of array.
    for( int i=0; i< numShapes; i++){
      shapes[i]= createShape( RECT, 0,0,100,100);
        }
        
   PShape      
 
```    

###Pass Array into Functions
Let's put this logic into a function:
Since arrays are objects, when we pass an object into a function we are actually passing the address of the object into the function, so anything done to elements of an array within a function are persisted to the object itself.  This is a good thing for us.


  ```java


//function to put a PShape object in each array element 
//shapes: PShape array
//size: dimensions for each PShape design

//Takes PShape array, populates each element with a PShape object
//size is a size parameter for the created PShape
void populateShapeList( PShape[ ] shapes, int size){
    int numShapes = shapes.length; //use length property of array.
   for( int i=0; i< numShapes; i++){
        PShape tempShape = vertexPattern1( length, hue);
        _shapes[ i ] = tempShape 
    } //end for-loop
} //end function

//function to create, and return a single vertex pattern 
PShape vertexPattern1( float length, int hue){
   PShape s = createShape();
   s.beginShape();
   s.fill( hue, 255, 255);
   s.vertex( 0,0);
   s.vertex( length, 0);
   s.vertex( length, length);
   s.endShape(CLOSE);
   return s;
}

  ```

###Display our shapes
In the code above, we've just stored a bunch of PShape objects, but we haven't drawn anything to the canvas using the shape( s, x, y) function for pshapes.

###Grid: Nested for-loops    

A pair of for-loops will allow us to ``iterate`` through the array to select each PShape object and set it's xy position for display.

We'll create nested for-loops:  

the outer for-loop controls which row is being created [ i ]

the inner loop creates determines which column [ j ] 

Inside this loop, we have both index values available [ i ][ j ]

   doSomething( arrayElement[ i ][ j ] );

###Rows: i,  Columns:  j
The code below shows nested for-loops to change xPos and yPos in a grid pattern, each time the inner loop code is executed, a single shape is displayed:  

**Display a single PShape from our shapes array:**

`shape( shapes[ shapeListIndex ], xPos, yPos);`

###Code to display 

   ```java
 
 
void displayShapes( PShape[] shapes, float cellSize,  int rows, int cols){
//variables to increment position and shapes in for-loop
  float xPos=0;  //s coordinate to draw each shape
  float yPos = 0;  //y coordinate to draw each shape
  int shapeListIndex = 0;  //keep track of current item to draw

  for( int i= 0; i< rows; i++){ //each row
    for( int j=0; j< cols; j++){
       shape(shapes[shapeListIndex], xPos,yPos);  //display Shape at xPos, yPos
       curIndex++;  //move to the next shape in the array
       xPos += cellSize; //move to next column
     }  //end j-loop
  xPos=0; //restart at col 0
  yPos += cellSize; //move yPositions down a row 
  } //end i=loop 
 
 }// end function


  ```

![](/assets/Screenshot 2017-09-22 14.51.04.png)


