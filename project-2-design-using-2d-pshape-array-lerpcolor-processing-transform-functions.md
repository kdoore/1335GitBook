#Project 2 - Design using 2D PShape Array, lerpColor, map, and Processing Transform Functions

For Project 2, students will create a Processing program to create custom 2D-Grid Artwork using 2 different PShape vertex patterns.  Project 2 builds on understanding learned in Project 1, creating PShape objects by specifying a set of vertex points.

Create a 2D Array of PShape objects,  create grid patterns using HSB colorMode and lerpColor to specify the color used.  If using color-selector tool, specify `colorMode(HSB, 360,100,100); //specify max range values` 

**Project Structure: Functions:**

** Step 1 - VertexShape Functions **   
- Create **2 functions** to create PShape vertex objects using float length, color foreground, and optional color: background as input parameters:

    PShape vertexShape1( float len, color foreground)
    
    PShape vertexShape2( float len, color foreground, color background);
   
    
###Example vertexShape code using PShape Group 
The code below uses PShape group functionality.  Multiple PShape objects can be layered to create a single PShape group object.  Below, 3 PShape objects are created, s1 and s are added as child objects to PShape g which is a group object.  The ordering that child objects are added to the group corresponds to the layer ordering for their display, s1 is designed as a background layer.

###PShape defined using len parameter - 

Here, PShapes are defined using vertices and the input parameter len , or some multiplicative factor times len.  Here, many vertices are defined using **len * .5**.  Since all vertices are defined in terms of the len input parameter, then we can vary the value of len when calling the function, and the displayed shape will be the same shape, but scaled at a different size depending on the value of len.

**Note: to define our vertices, we are using `len * factor`, we are not using `len + factor`.  By using a fractional value for `factor`, we're scaling the size of our pattern, since want to use len to control the size of our pattern.  If we add a factor, `len + factor`, that would create a position offset or `x,y`positioning of our pattern at the time we draw the pattern using the PShape: shape( s, x, y) function. **  

**PShape fill issues:** Please notice that s.fill(forground) might not work for all computers, in that case, rather than provide color at a vertex level, we should set fill as the first line in the vertexPattern function:  fill(foreground);
 
```java

PShape vertexShape1( float len, color foreground) {
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



```
###Test and Verify VertexPattern functions
After writing the vertexPattern functions, it's a good idea see what one of them looks like and to make sure they are displaying something, we can do this in setup

```java

void setup(){
size(600,600);
colorMode(HSB, 300,100,100);
color c1 = color(0, 255,255); //red
PShape testShape = vertexShape1( 100, c1); //hardcode value for len
shape( testShape, 300,300);//display at canvas center
}

 ```
 
** Step 2 - 2D Arrays of PShape Objects **     
 - Create at least 2 functions to create 2-Dimensional Arrays of PShape objects: these are the driver-functions that determine pattern logic, use colorLerp and map functions.  Suggestion: create and return PShape[][] objects within the function.


```java
   
PShape[][] populate2DArray( int rows, int cols,int size, color c1, color c2 ){
      PShape[][] shapesMatrix = new PShape[rows][cols];
      for( int i=0; i<rows; i++){
        for( int j=0; j< cols; j++){
          int k = i + j;  //diagonal index
          float colorAmount = map( k, 0, rows + cols-2, 0.0,1.0);
          color foreground = lerpColor( c1, c2, colorAmount);
          shapesMatrix[i][j] = vertexShape1(size,foreground); 
        }
       }
       return shapesMatrix;
}


//example use of function
//PShape[][] shapeMatrix1 = populate2DArray( rows, cols, size, c1, c2);

```

**Step 3 Display Primary Grid Function**
- Create functions to display each shapeMatrix.  These functions should take input parameters like:`PShape[][] shapes`, `int xPos`, `int yPos`, `int rows`, `int cols`, `int size`

**Step 4 Display Grid Function**

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

**Step 4 Display Grid in Other Regions**
###Use Rotate, Translate, Scale to display ShapeMatrix across other Regions.  
Within these functions, the canvas is transformed prior to calling the displayShapeMatrix code above. An example of using Rotate and Scale is shown for creating a ShapeMatrix in Region2.  Similar functions should be created for Region3 and Region4


```java
//display shapeMatrix in region2, use rotate( radians);
void displayRotateRegion2(PShape[][] shapesMatrix,int rows, int cols, int cellSize, int artWorkSize){
  pushMatrix();
  translate( artWorkSize, 0);
  rotate( PI/2);  //or rotate( radians(90));
  displayShapeMatrix(shapesMatrix, 0 ,0, rows , cols ,cellSize);
  popMatrix();
}

//similar code for Scaling in Region2
```

![](/assets/Screenshot 2017-09-28 13.26.58.png)

###Final Code Setup:
The code below shows the setup function where we're defining our variables and calling our functions, since there's no animation or interactivity in this project, setup can be used for organizing and executing our project logic.  

Now that we're creating smaller grid units and combining those to create a larger artwork, we need new variables to clarify these concepts.  I've decided the larger composition will be called the artWork, it has width = height = artWorkSize.  Each artwork is composed of 4 regions, where a 2D array of PShapes occupy one region of space. Each shapeMatrix in my  artwork has size defined by regionWidth = artworkSize/2, rows = 20, cols = 20. cellSize is defined as regionWidth/cols.

```java

void setup(){
  size(400,400);
  background(0);
  colorMode(HSB, 360,100,100);
  //DEFINE COLORS: 
  color c1= color( 71, 100, 100); //yellow-green
  color c2 = color(278,95,30);// dark purple
  color c3 = color(0); //black
  color c4=  color(200); //gray (white is 360)
  
 int artWorkSize=width;
 int regionWidth = artWorkSize/2;
  
  //dimensions for grid motif that occupies 1/4 size of the artWork 
  int rows = 20;
  int cols = rows;
  int cellSize = regionWidth/cols;
    
  //create smaller grid sections - 
  PShape[][] shapesMatrix1 = populate2DArray1(rows , cols ,cellSize, c1, c2  );
  PShape[][] shapesMatrix2 = populate2DArray2(rows , cols ,cellSize, c1, c2, c3, c4   );
  
  //add comments
  displayShapeMatrix(shapesMatrix1, 0 ,0, rows , cols ,cellSize);
  displayScaleRegion2(shapesMatrix2, rows , cols , cellSize, artWorkSize);
  displayScaleRegion3(shapesMatrix2, rows , cols , cellSize, artWorkSize);
  displayRotateRegion4(shapesMatrix1, rows , cols , cellSize, artWorkSize);
} 

```




