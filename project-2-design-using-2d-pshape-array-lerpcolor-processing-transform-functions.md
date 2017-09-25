#Project 2 - Design using 2D PShape Array, lerpColor, map, and Processing Transform Functions

For Project 2, students will create a Processing program to create custom 2D-Grid Artwork using 2 different PShape vertex patterns.  Project 2 builds on understanding learned in Project 1, creating PShape objects by specifying a set of vertex points.

Create a 2D Array of PShape objects,  create grid patterns using HSB colorMode and lerpColor to specify the color used.  If using color-selector tool, specify colorMode(HSB, 360,100,100);

**Project Structure: Functions:**

1.  Create 2 functions to create PShape vertex objects using float length, color foreground, and optional color: background as input parameters:

    `PShape vertexPattern1( float len, color foreground)`
    
    `PShape vertexPattern2( float len, color foreground, color background);`
    
2.  Create 2 functions to create 2-Dimensional Grids of PShape objects: these are the driver-functions that determine pattern logic, use colorLerp and map functions.


```java
   
PShape[][] populateGradientDiaGrid( int rows, int cols,int size, color c1, color c2 ){
      PShape[][] shapesMatrix = new PShape[rows][cols];
      for( int i=0; i<rows; i++){
        for( int j=0; j< cols; j++){
          float colorAmount = map( i+j, 0, rows + cols, 0.0,1.0);
          color foreground = lerpColor( c1, c2, colorAmount);
          shapesMatrix[i][j] = vertexPattern1(size,foreground); 
        }
       }
       return shapesMatrix;
}

PShape[][] populateGradientDiaGrid2( int rows, int cols,int size, color c1, color c2, color c3, color c4 ){
      PShape[][] shapesMatrix = new PShape[rows][cols];
      for( int i=0; i<rows; i++){
        for( int j=0; j< cols; j++){
          float colorAmount = map( i+j, 0, rows + cols, 0.0,1.0);
          color foreground = lerpColor( c1, c2, colorAmount);
          color background = lerpColor( c3, c4, colorAmount);
          shapesMatrix[i][j] = vertexPattern2(size,foreground, background ); 
        }
       }
       return shapesMatrix;
}

```


3. 




