#Transforms for Position, Rotation, Scale of ShapeMatrix Elements

We can use the Processing transform functions to position  our shapeMatrix elements when we are ready to create our design composition.

To create a complete artwork, we can take several simple 2D grids and position them adjacent to each other to form a larger artwork composition.  There are several ways to reorient the blocks to create interesting design patterns.

###Rotation of Grid Units:
Given a single grid unit positioned at the canvas origin, let's look at the result of rotations of a single grid unit through 90, 180, and 270 degrees, where rotation always occurs around the canvas origin.

![](/assets/Screenshot 2017-09-27 21.27.32.png)

The image above shows that a combination of rotation and translation can be used to create design patterns from a single grid module.  When writing these display functions.  

###Example code for Region2 Grid - Rotate 90 degrees


```java
void displayRotateRegion2(PShape[][] shapesMatrix,int rows, int cols, int cellSize, int artWorkSize){
  pushMatrix();
  translate( artWorkSize, 0);
  rotate( PI/2);
  displayShapeMatrix(shapesMatrix, 0 ,0, rows , cols ,cellSize);
  popMatrix();
}
```

###Example code for Region2 Grid  - Scale( -1.0, 1.0);


```java
void displayRotateRegion2(PShape[][] shapesMatrix,int rows, int cols, int cellSize, int artWorkSize){
  pushMatrix();
  translate( artWorkSize, 0);
  scale(-1.0, 1.0);
  displayShapeMatrix(shapesMatrix, 0 ,0, rows , cols ,cellSize);
  popMatrix();
}
```


