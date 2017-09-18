#PShape Objects in a Grid Layout

The first approach for creating grid designs will use an ``Array`` of PShape Objects and nested ``for-loops`` to control x,y positioning of each PShape object.

###Declare and Initialize an Array of PShape Objects

The syntax to create an array of PShape objects is: 
    1. Declare the array:  ``PShape[ ] myShapes``;
    2. In setup:  initialize the array by specifying the number of elements.
    
   
   

```java
 
    PShape[ ] myShapes;
    int rows = 10;
    int cols = 10;
    
    void setup(){
       size( 400,400);
       //we need rows * cols shapes to fill the grid
       myShapes = new PShape[ rows * cols ];
     
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


```java

void populateShapeList( PShape[ ] shapes){
    int numShapes = shapes.length; //use length property of array.
   for( int i=0; i< numShapes; i++){
        _shapes[ i ] = createShape(ELLIPSE,    0,0,cellSize-10,cellSize-5);

   }
}

```


###Display our shapes
In the code above, we've just stored a bunch of PShape objects, but we haven't drawn anything to the canvas using the shape( s, x, y) function for pshapes.  

A set of for-loops will allow us to ``iterate`` through the array to select each PShape object and set it's xy position for display.

###Rows: i,  Columns:  j


 ```java
 
void displayShapes( PShape shapes){

float xPos=0;
float yPos = 0;
int curIndex = 0;
float size = width / rows;  //each grid's size

for( int i= 0; i< rows; i++){ //each row
    for( int j=0; j< cols; j++){
       shape(shapes[curIndex], xPos,yPos);
       curIndex++;
       xPos+= size; //move to next column
     }  //end j-loop
  xPos=0; //restart at col 0
  yPos += size; //move down a row 
 } //end i=loop 
 
 }// end function

```




