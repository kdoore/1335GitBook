#Animation for ShapeMatrix

In order to animate anything in Processing, the draw( ) function must be included in your project.  Within the draw( ) function, some parameters of the design must be changing over time, such as size, color.  frameCount, modulus can be used to create a timer that controls animation of size, color.

###Animate: PShape Color, Length (size)

**Animation - cycle through ranges**
For animation of shape patterns, it will be convenient to have color and size repeatedly cycle through a fixed range of colors and size. 

- CellSize - create a changing fraction to animate size 
- Color: - create a changing fraction to animate lerpColor

###FrameCount timer
We can use frameCount, modulus to create a timer that cycles from 0 to some maxValue.

```java
float maxTime = 100;
float fractionSize = map(frameCount%maxTime, 0, maxTime, 0.2,1.0)
cellSize = cellSize * fractionSize;
```
**can be used to increase the size beyond cellSize**

```java
 float fractionSize = map(frameCount%maxTime, 0, maxTime, 0.2,2.0) 
    //fraction is larger than 1.0, so size will be doubled
```
Similar logic to above, but this will cause the fraction to range from .2 to 2.0, since the map function extends the mapping for values outside the range. 

```java

float halfMax = maxTime/2;
    float fractionSize2 = map(frameCount%maxTime, 0, halfMax, 0.2,1.0)
```

Similar logic can be used to create animated color by using map to create a 

float fractionLerp = map(frameCount%maxTime, 0, maxTime, 0.0,1.0) ;  //for lerpColor, keep range: 0.0-1.0


![](/assets/Screen Shot 2019-10-15 at 12.02.44 PM.png)


####Move code into the draw function for animation
####Added logic: mousePressed for noLoop(), keyPressed for loop()

##Animation Code:

```java
void setup() {
  size( 800, 800);
  colorMode(HSB, 360, 100, 100);
  background(0);
  
}


void setup() {
  size( 400, 400);
  colorMode(HSB, 360, 100, 100);
  background(0);
  
}


void draw(){
   //fade background 
   fill( 0, 5); //transparant black
   rect( 0,0,width, height);
  
  if(mousePressed){
    noLoop();
  }
  
  
  float artWorkSize = width;
  float regionSize = artWorkSize/2;
  
  int rows = 10;
  int cols = 10;
  float cellSize = regionSize/cols;
  
  color purple = color( 290, 100, 100);
  color aqua = color(180, 100, 100);
  
  float maxFC = 100; //max value for frameCount timer
  float fractionSize = map(frameCount%maxFC,0 , maxFC, .2, 2.0); //makes larger 
  float fractionColor = map((frameCount%maxFC),0 , maxFC, 0.0, 1.0);
  
  ///use mouseX to create interactive accent color
  float hueMx = map( mouseX, 0, width, 120,250); //color change with mouseX movement
  color accentMx = color( hueMx, 100,100);
  color curColor = lerpColor( accentMx,aqua, fractionColor);
 
  PShape[][] myShapes = new PShape[rows][cols]; //num elements is rows*cols
  populate2DArray( myShapes, rows, cols, cellSize* fractionSize, purple, curColor);
 
 //display in region1 at smaller (1/4) scale
  pushMatrix();
  scale( 1, 1);
  displayShapeMatrix( myShapes, rows, cols, cellSize);
  popMatrix();
  

  //region2
 mirrorRegion2(myShapes, rows, cols, cellSize, artWorkSize);    
  

  //region3
  pushMatrix();
  translate(0, height); //move origin to upper right
  scale( 1, -1); //mirror across x-axix, make smaller
  displayShapeMatrix( myShapes, rows, cols, cellSize);
  popMatrix();
  
  //region4
  pushMatrix();
  translate(width, height); //move origin to upper right
  scale( -1, -1); //mirror across origin and make smaller
  displayShapeMatrix( myShapes, rows, cols, cellSize);
  popMatrix();
} //end draw

//press any key to restart animation
void keyPressed(){
  loop();
}

void mirrorRegion2(PShape[][] shapes, int rows, int cols, float cellSize, float artWorkSize  ){
   pushMatrix();
  translate(artWorkSize, 0); //move origin to upper right
  scale( -1, 1); //mirror and scale smaller 
  displayShapeMatrix( shapes, rows, cols, cellSize);
  popMatrix();
  
}


void displayShapeMatrix( PShape[][] shapes, int rows, int cols, float cellSize ) {
  int xPos=0;
  int yPos=0;
  for ( int i=0; i< rows; i++) {
    for ( int j=0; j< cols; j++) {
      shape( shapes[i][j], xPos, yPos); //display one shape
      xPos += cellSize;
    }//end inner loop - cols
    xPos = 0; //reset xPos to 0 for next row
    yPos += cellSize;
  } //end outer loop - rows
}//end function


void populate2DArray( PShape[][] shapes, int rows, int cols, float cellSize, color c1, color c2 ) {
  for ( int i=0; i< rows; i++) {
    for ( int j=0; j< cols; j++) {
      int k= i+j; //used for a diagonal pattern
      int l= min( i, j); //concentric pattern
      float fractionk = map( k, 0, rows+cols-2, 0.0, 1.0);
      float fractionl= map( l, 0, rows-1, 0.0, 1.0);
      //use fractions to create color gradient patterns
      color colorK = lerpColor( c1, c2, fractionk); //diagonal gradient
      color colorL = lerpColor(color(0), c1, fractionl); //concentric color
      PShape curShape; //create a shape
      if ( k%2==0) {
        curShape= createPosShape( cellSize* 2.0, colorK); //make cutout shape larger
      } else {
        curShape = createShape(GROUP);
        recursiveShapes( curShape, cellSize*.6, 3, colorL); //make circles smaller
      } //end if-else
      shapes[i][j] = curShape; //set the shape as the array element
    }//end inner for-loop - cols
  }//end outer for-loop - rows
}//end function populate2DArray

void recursiveShapes(PShape group,  float len, int level, color c1   ){
  if( level <0){
    return;
  }
  color curColor = color( hue( c1), saturation(c1), brightness(c1) *.8);
  PShape s = createEllipse( len, curColor);
  group.addChild(s);
  recursiveShapes( group, len*.8, level-1, curColor);
}


PShape createEllipse( float len, color c1){
  PShape s = createShape(ELLIPSE, 0, 0, len, len); //rect if k is even
  s.setFill(c1);
  return s;
}



PShape createPosShape( float len, color c1){
  PShape s = createShape();
  s.beginShape();
  s.fill(c1 ); //HSB - blue full sat, bright
  s.vertex( 0,0); //point 1 for outer shape (clock-wise rotation for drawing points)
  s.vertex( len*.4,0); //point  2
  s.vertex( len*.6, len*.6); //point 3
  s.vertex( 0, len*.4); //point 4
  s.vertex( 0,0); //last point for outer shape

   ////start of inner cutout - counter-clockwise ordering
  s.beginContour(); //make internal cutout 
  s.vertex( len*.25,len*.45); //inner cutouts - point 5
  s.vertex(len*.5, len*.5);  //point 6
  s.vertex( len*.45, len*.25); //point 7
  s.endContour(); //end internal cutout

  s.endShape(CLOSE); //end shape
  return s; 
}
```




