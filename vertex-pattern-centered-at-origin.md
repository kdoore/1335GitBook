#Vertex Pattern Centered at the Origin

If we want a Vertex Pattern centered at the origin, so that each time we call the `vertexPattern( len ) `function, with a different value for the `len parameter`, we'll have a concentric set of shapes, then we need to define our vertex pattern with it's center point at ( 0, 0).  This means that if the pattern is drawn at the canvas origin, only the lower-right quadrant of our design will show.  For this project, that's ok, since we'll be drawing the pattern at the current mouse position.   

###VertexPattern defined by a single length parameter
Just as with previous examples, once again, we'll define our shape's vertices so they are defined relative to a single, length, parameter.  In this case, we want our shape to be enclosed in a square of size length x length.  However, in this case, we're going to have our shape's vertices offset, so the point 0,0 is at the center of our design. 

 
###VertexPattern with Center at Origin: 0,0
The image below shows that if we want to maintain the full size of our pattern as width = height = len, with the center at 0,0, then we need to specify our vertices as ranging from (-len/2, -len/2 ) at the top left corner, to (len/2, len/2) at the bottom right corner.  The VertexPattern function to define this shape is shown below the image, where 9 vertex points are created, starting and ending at the point (0,0);

  ![](/assets/Screen Shot 2018-01-29 at 1.08.09 PM.png)
  


```java

void vertexPattern( float len){
  PShape s = createShape();
  s.beginShape();
  s.fill(0 ,100, len ); //fully saturated red, with brightness set by len
  s.vertex(0,0);
  s.vertex(len/4,0);
  s.vertex( len/2, len/2);
  s.vertex(0, len/4);
  s.vertex( 0,0);
  s.vertex(-len/4, 0);
  s.vertex( -len/2, -len/2);
  s.vertex( 0, -len/4);
  s.vertex(0,0);
  s.endShape(CLOSE);
  shape(s, 0,0); //this draws the shape at (0,0)
}   ///end vertexPattern
  

```

###Processing Coordinate System:  
The processing coordinate system has the x-axis increase to the right, but the y-axis increases in the downward direction, this is not the same as the cartesian coordinate system that we are familiar with. Therefore , we need to be careful with the sign (+, - ) of each vertex point.  Follow the guidelines below.

  -  upper-left quadrant:  _negative x , negative y_
  -  upper-right quadrant: _positive x, negative y_     
  -  lower-right quadrant:  _positive x, positive y _ 
  -  lower-left quadrant:  _negative x, positive y _
  
  