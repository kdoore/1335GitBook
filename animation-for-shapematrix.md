#Animation for ShapeMatrix

In order to animate anything in Processing, the draw( ) function must be included in your project.  Within the draw( ) function, some parameters of the design must be changing over time.

###Animate: PShape Color, Length (size)

**Animation - cycle through ranges**
For animation of shape patterns, it will be convenient to have color and size repeatedly cycle through a fixed range of colors and size. 

CellSize:  minSize, maxSize
Color: lerpColor


**Animation: Modifying 2D-Arrays of PShape Data**
Within the draw( ) function (for each frame of animation execution)  - It is necessary to **re-create the 2DArray of PShapes**, because the PShapes size and color stored as part of the PShape within the 2D array of PShapes.  

Animation requires repeated execution of the following functions:  

Repeat-Execution:  Populate2DArray( )
Repeat-Execution:  DisplayShapeMatrix() for each grid region 

We can create a new function that calculates changing size and colors and then calls Populate2DArray and DisplayShapeMatrix( ) with these new values. 

