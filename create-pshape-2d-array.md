#Create 2D Array of PShapes
In the code below, we'll modify our [simple 2D arrays project](/2d-arrays-with-lerpcolor.md) so that we're now creating PShape objects for each 2D Array element (instead of using processing rect()), then we'll display those PShape in a second step of the process.

###PShape[ ][ ] ShapeMatrix
In the code below, we'll create a 2D array of PShapes using the Processing PShape methods, we'll use the calculated gradient color to PShape: setFill( color ) method for each PShape. Then we'll before display each PShape using the PShape: shape( PShape, x, y ) method 

