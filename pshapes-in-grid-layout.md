#PShape Objects in a Grid Layout

The first approach for creating grid designs will use an array of PShape Objects and nested for-loops to control x,y positioning of each PShape object.

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
    
    