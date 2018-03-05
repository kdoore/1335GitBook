#Function: DisplayShapeMatrix( )

In this section, we will refactored the code to create a custom function: DisplayShapeMatrix( ), that can draw a 2D PShape array in a grid layout, at any x

The function below is used to determine the grid-layout, and actually calls the PShape `shape( ) `function that is used to render each PShape object on the screen.



```java

void displayShapeMatrix(PShape[][] shapes, int x , int y , int rows, int cols, int size){      
 
 pushMatrix();  //save any prior transforms  
 
 translate( x , y );   //change origin location 
 int xPos=0;   
 int yPos=0;          
 for( int i=0; i< rows; i++){        
    for( int j=0; j< cols; j++){          shape(shapes[i][j], xPos, yPos);          
    xPos += size;        
    }         
     xPos =0;        
     yPos += size;      
     }  
  popMatrix(); // undo transforms up to prior pushMatrix()
  }
```

