#Function: DisplayShapeMatrix( )
The function below

```java

void displayShapeMatrix(PShape[][] shapes, int xPos, int yPos, int rows, int cols, int size){  pushMatrix();  translate( xPos, yPos);   int x=0;   int y=0;      for( int i=0; i< rows; i++){        for( int j=0; j< cols; j++){          shape(shapes[i][j], x, y);          x += size;        }          x =0;        y += size;      }  popMatrix();}
```

