# Function: DisplayShapeMatrix()

In this section, we will refactor the code to create a custom function: displayShapeMatrix( ), that can render a 2D PShape array in a grid layout, at any x,y location.

The function below is used to determine the grid-layout, and actually calls the PShape `shape( )`function that is used to render each PShape object on the screen.

```java
void displayShapeMatrix(PShape[][] shapes,int rows, int cols, int size){
 int xPos=0;  
 int yPos=0;         
 for( int i=0; i< rows; i++){     
  for( int j=0; j< cols; j++){   
   shape(shapes[i][j], xPos, yPos);         
    xPos += size;      
    }  //end inner for-loop (j:cols)     
    xPos =0;       
    yPos += size;     
  } //end outer for-loop (i:rows)
 } //end function
```
