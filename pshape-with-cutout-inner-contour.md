#PShape with Cut-out, Inner-contour

![](/assets/Screen Shot 2018-09-04 at 12.22.32 PM.png)

###PShape with Contour
The code below shows that PShape can have an inner cutout created using the beginContour(), endContour() functions.  The vertex points specified within those 2 functions will be cut-out of the larger shape that was specified before the beginContour() function.



```java
  PShape s = createShape();
  s.beginShape();
  s.fill(200, 100,100 ); //HSB - blue full sat, bright
  s.vertex( 0,0); //point1 for outer shape (clock-wise rotation for drawing points)
  s.vertex( len*.4,0);
  s.vertex( len*.6, len*.6);
  s.vertex( 0, len*.4);
  s.vertex( 0,0); //last point for outer shape
 
   ////start of inner cutout - counter-clockwise ordering
  s.beginContour(); //make internal cutout 
  s.vertex( len*.25,len*.45); //inner cutouts
  s.vertex(len*.5, len*.5);
  s.vertex( len*.45, len*.25);
  s.endContour(); //end internal cutout
  
  s.endShape(CLOSE); //end shape
  shape( s, 0,0);  //this displays the shape on the canvas at point (0,0)

```
###Repeat Pattern using PShape with contour
The image below shows an intricate pattern created using a recursive function and a PShape that has an inner cut-out, contour.

![](/assets/Screen Shot 2018-09-04 at 12.17.58 PM.png)



