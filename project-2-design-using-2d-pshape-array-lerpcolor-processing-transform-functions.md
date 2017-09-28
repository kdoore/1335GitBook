#Project 2 - Design using 2D PShape Array, lerpColor, map, and Processing Transform Functions

For Project 2, students will create a Processing program to create custom 2D-Grid Artwork using 2 different PShape vertex patterns.  Project 2 builds on understanding learned in Project 1, creating PShape objects by specifying a set of vertex points.

Create a 2D Array of PShape objects,  create grid patterns using HSB colorMode and lerpColor to specify the color used.  If using color-selector tool, specify `colorMode(HSB, 360,100,100); //specify max range values` 

**Project Structure: Functions:**

1.Create 2 functions to create PShape vertex objects using float length, color foreground, and optional color: background as input parameters:

    PShape vertexPattern1( float len, color foreground)
    
    PShape vertexPattern2( float len, color foreground, color background);
   
    
###Example vertexPattern code using PShape Group 
The code below uses PShape group functionality.  Multiple PShape objects can be layered to create a single PShape group object.  Below, 3 PShape objects are created, s1 and s are added as child objects to PShape g which is a group object.  The ordering that child objects are added to the group corresponds to the layer ordering for their display, s1 is designed as a background layer.
 
```java

PShape vertexPattern1( float len, color foreground) {
  PShape s = createShape( );
  s.beginShape();
  s.fill(foreground);
  s.vertex(len/2, len/2);
  s.vertex( 0, 0);
  s.vertex(len, 0);
  s.vertex( len/2, len/2);
  s.vertex( len, len);
  s.vertex(0, len);
  s.vertex( len/2, len/2);
  s.endShape(CLOSE);
  return s;
}  //end createOneShape

//Use PShapes Group to add Background PShape
PShape vertexPattern2( float len, color foreground, color background) {
  PShape s1 = createShape( RECT,0,0,len,len);
  s1.setFill( background);
  PShape s = createShape( );
  s.beginShape();
  s.fill(foreground);
  s.vertex(len/2, len/2);
  s.vertex( 0, 0);
  s.vertex(len, 0);
  s.vertex( len/2, len/2);
  s.vertex( len, len);
  s.vertex(0, len);
  s.vertex( len/2, len/2);
  s.endShape(CLOSE);
  PShape g = createShape(GROUP);
  g.addChild(s1);
  g.addChild(s);
  return g;
}  //end createOneShape



```
    
2.Create at least 2 functions to create 2-Dimensional Grids of PShape objects: these are the driver-functions that determine pattern logic, use colorLerp and map functions.  Suggestion: create and return PShape[][] objects within the function.


```java
   
PShape[][] populateGradientGrid( int rows, int cols,int size, color c1, color c2 ){
      PShape[][] shapesMatrix = new PShape[rows][cols];
      for( int i=0; i<rows; i++){
        for( int j=0; j< cols; j++){
          int k = i + j;  //diagonal index
          float colorAmount = map( k, 0, rows + cols, 0.0,1.0);
          color foreground = lerpColor( c1, c2, colorAmount);
          shapesMatrix[i][j] = vertexPattern1(size,foreground); 
        }
       }
       return shapesMatrix;
}

PShape[][] populateGradientGrid2( int rows, int cols,int size, color c1, color c2, color c3, color c4 ){
      PShape[][] shapesMatrix = new PShape[rows][cols];
      for( int i=0; i<rows; i++){
        for( int j=0; j< cols; j++){
          int k = i + j; //diagonal index
          float colorAmount = map( k, 0, rows + cols, 0.0,1.0);
          color foreground = lerpColor( c1, c2, colorAmount);
          color background = lerpColor( c3, c4, colorAmount);
          shapesMatrix[i][j] = vertexPattern2(size,foreground, background ); 
        }
       }
       return shapesMatrix;
}

//example function call:

PShape[][] shapeMatrix1 = populateGradientGrid1( rows, cols, size, c1, c2);

```


3. Create functions to display each shapeMatrix.  These functions should take input parameters like:`PShape[][] shapes`, `int xPos`, `int yPos`, `int rows`, `int cols`, `int size`

Use processing transform functions to translate the origin to the position where the shapeMatrix should be displayed.  Add rotation if needed to re-orient the shapeMatrix.  

The code below has simple logic to step through each shapes[][] element and display it using the nested for loop to change the position of x and y across rows and columns.

```java

void displayShapeMatrix(PShape[][] shapes, int xPos, int yPos, int rows, int cols, int size){
  pushMatrix();
  translate( xPos, yPos);
   int x=0;
   int y=0;
      for( int i=0; i< rows; i++){
        for( int j=0; j< cols; j++){
          shape(shapes[i][j], x, y);
          x += size;
        }  
        x =0;
        y += size;
      }
  popMatrix();
}

```

###Use Rotate, Translate, Scale to display ShapeMatrix across other Regions.  
Within these functions, the canvas is transformed prior to calling the displayShapeMatrix code above. An example of using both Rotate and Scale are shown, for creating a ShapeMatrix in Region2.  Similar functions should be created for Region3 and Region4


```java
//display shapeMatrix in region2, use rotate( radians);
void displayRotateRegion2(PShape[][] shapesMatrix,int rows, int cols, int cellSize, int artWorkSize){
  pushMatrix();
  translate( artWorkSize, 0);
  rotate( PI/2);  //or rotate( radians(90));
  displayShapeMatrix(shapesMatrix, 0 ,0, rows , cols ,cellSize);
  popMatrix();
}

//display shapeMatrix in Region2, use scale(scaleX, scaleY);
void displayScaleRegion2(PShape[][] shapesMatrix,int rows, int cols, int cellSize, int artWorkSize){
  pushMatrix();
  translate( artWorkSize, 0);
  scale( -1.0, 1.0);
  displayShapeMatrix(shapesMatrix, 0 ,0, rows , cols ,cellSize);
  popMatrix();
}

```

![](/assets/Screenshot 2017-09-28 13.26.58.png)

###Final Code Setup:


```java

void setup(){
  size(400,400);
  background(0);
  colorMode(HSB, 360,100,100);
  color c1= color( 71, 100, 100); //chartruse
  color c2 = color(278,95,30);// bright purple
  
  int artWorkRows = 20; //even number - rows, cols
  int artWorkCols= artWorkRows;
  int artWorkSize=400;
  int cellSize = artWorkSize/artWorkRows;
  
  //dimensions for grid motif that occupies 1/4 size of the artWork 
  int rows = artWorkRows/2;
  int cols = artWorkCols/2;
  
  //create smaller grid sections - 
  PShape[][] shapesMatrix1 = populateGradientGrid(rows , cols ,cellSize, c1, c2  );
  PShape[][] shapesMatrix2 = populateGradientGrid2(rows , cols ,cellSize, c1, c2   );
  
  //add comments
  displayShapeMatrix(shapesMatrix1, 0 ,0, rows , cols ,cellSize);
  displayScaleRegion2(shapesMatrix2, rows , cols , cellSize, artWorkSize);
  displayScaleRegion3(shapesMatrix2, rows , cols , cellSize, artWorkSize);
  displayRotateRegion4(shapesMatrix1, rows , cols , cellSize, artWorkSize);
} 

```





