#Transforms for Position, Rotation, Scale of ShapeMatrix Elements

We can use the Processing transform functions to position  our shapeMatrix elements when we are ready to create our design composition.

To create a complete artwork, we can take several simple 2D grids and position them adjacent to each other to form a larger artwork composition.  There are several ways to reorient the blocks to create interesting design patterns.

###Rotation of Grid Units:
Given a single grid unit positioned at the canvas origin, let's look at the result of rotations of a single grid unit through 90, 180, and 270 degrees, where rotation always occurs around the canvas origin.

![](/assets/Screenshot 2017-09-28 09.36.59.png)

The image above shows that a combination of rotation and translation can be used to create design patterns from a single grid module.  When writing these display functions.  Region1 shows the position of the origin at the upper left corner.  The larger, light-blue square located to the upper left of region 1 uses simple rotation to create a larger composition from a single unit.  

The larger, light green square to the lower right of region 1 uses translation and rotation to form a larger composition using repetition of the basic square unit shown in region1.  The yellow circles show where the origin has been translated.  The red circle shows the canvas origin where the original Region1 square is positioned. The code below shows the transformations required for positioning the square at the Region2 location using rotation and translation. When using an asymmetric design, this method of repetition shows rotational asymmetry.

###Example code for Region2 Grid - Rotate 90 degrees


```java
void displayRotateRegion2(PShape[][] shapesMatrix,int rows, int cols, int cellSize, int artWorkSize){
 int w= artWorkSize;
  pushMatrix();
  translate( w, 0);
  rotate( PI/2);  // same as: rotate(radians( 90));
  displayShapeMatrix(shapesMatrix, 0 ,0, rows , cols ,cellSize);
  popMatrix();
}
```
###Mirroring - Using Processing scale( x, y)

In some situations, rotation of the grid doesn't provide the desired repetition configuration.  If your design requires mirroring about an axis, then the Processing scale transformation functions can be useful.  The image below uses `scale( scaleX, scaleY)` along with translate( )  to achieve similar results as the with rotate, but results in mirroring the pattern.  

![](/assets/Screenshot 2017-09-28 09.34.56.png)

###Example code for Region2 Grid  - Scale( -1.0, 1.0);

```java
void displayRotateRegion2(PShape[][] shapesMatrix,int rows, int cols, int cellSize, int artWorkSize){
  int w= artWorkSize;
  pushMatrix();
  translate( w, 0);
  scale(-1.0, 1.0);
  displayShapeMatrix(shapesMatrix, 0 ,0, rows , cols ,cellSize);
  popMatrix();
}
```



