#Project 2 - Design using 2D PShape Array, lerpColor, map, and Processing Transform Functions

For Project 2, students will create a Processing program to create custom 2D-Grid Artwork using 2 different PShape vertex patterns.  Project 2 builds on understanding learned in Project 1, creating PShape objects by specifying a set of vertex points.

Create a 2D Array of PShape objects,  create grid patterns using HSB colorMode and lerpColor to specify the color used.  If using color-selector tool, specify `colorMode(HSB, 360,100,100); //specify max range values` 

**Project Structure: Functions:**

1.Create 2 functions to create PShape vertex objects using float length, color foreground, and optional color: background as input parameters:

    PShape vertexPattern1( float len, color foreground)
    
    PShape vertexPattern2( float len, color foreground, color background);
   
    
###Example vertexPattern code using PShape Group 
The code below uses PShape group functionality.  Multiple PShape objects can be layered to create a single PShape group object.  Below, 3 PShape objects are created, s1 and s are added as child objects to PShape g which is a group object.  The ordering that child objects are added to the group corresponds to the layer ordering for their display, s1 is designed as a background layer.

###PShape defined using len parameter - 

Here, PShapes are defined using vertices and the input parameter len , or some multiplicative factor times len.  Here, many vertices are defined using **len * .5**.  Since all vertices are defined in terms of the len input parameter, then we can vary the value of len when calling the function, and the displayed shape will be the same shape, but scaled at a different size depending on the value of len.

**Note: to define our vertices, we are using `len * factor`, we are not using `len + factor`.  By using a fractional value for `factor`, we're scaling the size of our pattern, since want to use len to control the size of our pattern.  If we add a factor, `len + factor`, that would create a position offset or `x,y`positioning of our pattern at the time we draw the pattern using the PShape: shape( s, x, y) function. **  

**PShape fill issues:** Please notice that s.fill(forground) might not work for all computers, in that case, rather than provide color at a vertex level, we should set fill as the first line in the vertexPattern function:  fill(foreground);
 
```java

PShape vertexPattern1( float len, color foreground) {
  //fill(foreground); ///alternative way to set the PShape color
  PShape s = createShape( );
  s.beginShape();
  s.fill(foreground);
  s.vertex(len * .5, len * .5);
  s.vertex( 0, 0);
  s.vertex(len, 0);
  s.vertex( len * .5, len * .5);
  s.vertex( len, len);
  s.vertex(0, len);
  s.vertex( len * .5, len * .5);
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
###Test and Verify VertexPattern functions
After writing the vertexPattern functions, it's a good idea see what one of them looks like and to make sure they are displaying something, we can do this in setup

```java

void setup(){
size(600,600);
colorMode(HSB, 300,100,100);
color c1 = color(0, 255,255); //red
PShape testShape = vertexPattern1( 100, c1); //hardcode value for len
shape( testShape, 300,300);//display at canvas center
}

 ```
 
       
2.Create at least 2 functions to create 2-Dimensional Grids of PShape objects: these are the driver-functions that determine pattern logic, use colorLerp and map functions.  Suggestion: create and return PShape[][] objects within the function.


```java
   
PShape[][] populateGradientGrid( int rows, int cols,int size, color c1, color c2 ){
      PShape[][] shapesMatrix = new PShape[rows][cols];
      for( int i=0; i<rows; i++){
        for( int j=0; j< cols; j++){
          int k = i + j;  //diagonal index
          float colorAmount = map( k, 0, rows + cols-2, 0.0,1.0);
          color foreground = lerpColor( c1, c2, colorAmount);
          shapesMatrix[i][j] = vertexPattern1(size,foreground); 
        }
       }
       return shapesMatrix;
}

PShape[][] populateGradientGrid2( int rows, int cols,int size, color c1, color c2, color c3, color c4 ){
      PShape[][] shapesMatrix = new PShape[rows][cols];
      for( int i=0; i < rows; i++){
        for( int j=0; j< cols; j++){
          int k = i + j; //diagonal index
          // adjust the map function variables to change design features
          float colorAmount = map( k, 0, (rows + cols - 2), 0.0,1.0);
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

void displayShapeMatrix(PShape[][] shapes, int x , int y , int rows, int cols, int size){
  pushMatrix();
  translate( x , y );
   int xPos=0;
   int yPos=0;
      for( int i=0; i< rows; i++){
        for( int j=0; j< cols; j++){
          shape(shapes[i][j], xPos, yPos);
          xPos += size;
        }  
        xPos =0;
        yPos += size;
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
The code below shows the setup function where we're defining our variables and calling our functions, since there's no animation or interactivity in this project, setup can be used for organizing and executing our project logic.  

Now that we're creating smaller grid units and combining those to create a larger artwork, we need new variables to clarify these concepts.  I've decided the larger composition will be called the artWork, it has width = height = artWorkSize.  It is no longer true that the artWorkSize is the same as the processing canvas size, as we'll want room around our artWork to put design tools that we create.  I also define artWorkRows and artWorkCols, this is to create a distinction between the rows and cols that are used for creating a PShape[][] shapes matrix, that will be likely be smaller than the full artWorkSize.  Each shapeMatrix in my  artwork has rows = artWorkRows / 2, cols = artWorkCols / 2.

```java

void setup(){
  size(400,400);
  background(0);
  colorMode(HSB, 360,100,100);
  color c1= color( 71, 100, 100); //chartruse
  color c2 = color(278,95,30);// bright purple
  color c3 = color(0);
  color c4=  color(200);
  
  int artWorkRows = 20; //even number - rows, cols
  int artWorkCols= artWorkRows;
  int artWorkSize=400;
  int cellSize = artWorkSize/artWorkRows;
  
  //dimensions for grid motif that occupies 1/4 size of the artWork 
  int rows = artWorkRows/2;
  int cols = artWorkCols/2;
  
  //create smaller grid sections - 
  PShape[][] shapesMatrix1 = populateGradientGrid(rows , cols ,cellSize, c1, c2  );
  PShape[][] shapesMatrix2 = populateGradientGrid2(rows , cols ,cellSize, c1, c2, c3, c4   );
  
  //add comments
  displayShapeMatrix(shapesMatrix1, 0 ,0, rows , cols ,cellSize);
  displayScaleRegion2(shapesMatrix2, rows , cols , cellSize, artWorkSize);
  displayScaleRegion3(shapesMatrix2, rows , cols , cellSize, artWorkSize);
  displayRotateRegion4(shapesMatrix1, rows , cols , cellSize, artWorkSize);
} 

```




