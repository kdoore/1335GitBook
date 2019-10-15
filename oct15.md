##Oct 15, F19  
####modified - uses only 1 PShape, simplified color-pattern logic 
####Includes Recursive Pattern Function, Refactored Mirroring Logic, ArtWorkSize

![](/assets/Screen Shot 2019-10-15 at 11.40.12 AM.png)

```java

void setup() {
  size( 600, 600);
  colorMode(HSB, 360, 100, 100);
  background(0);
  color purplePie = color( 280, 100, 100); //MUST USE CUSTOM COLORS, COLOR Names
  color aquaTot = color(200, 100, 100); //MUST USE CUSTOM COLORS, COLOR Names
  
  float artWorkSize = width;
  float regionSize = artWorkSize/2;
  
  int rows = 10;
  int cols = 10;
  float cellSize = regionSize/cols;
  
  PShape[][] myShapes = new PShape[rows][cols]; //num elements is rows*cols
  populate2DArray( myShapes, rows, cols, cellSize, purplePie,aquaTot);
  
  //option: Create additional pattern logic for asymetric shapeMatrix 
  //PShape[][] myShapes2 = new PShape[rows][cols]; //create 2nd 2D array with different pattern logic
  //populate2DArray2( myShapes2, rows, cols, cellSize, purple, aqua);
  //mirrorRegion2( myShapes2, rows, cols, cellSize, artWorkSize);  //display in region 2

 //display in region1 
  displayShapeMatrix( myShapes, rows, cols, cellSize);
  
  
  //region2
   
  //display shapeArray in region2
  mirrorRegion2(myShapes, rows, cols, cellSize, artWorkSize);    
  

  //region3
  //put this code in new function
  pushMatrix();
  translate(0, height); //move origin to upper right
  scale( 1, -1); //mirror across x-axix, make smaller
  displayShapeMatrix( myShapes, rows, cols, cellSize);
  popMatrix();
  
  //region4
  //put this code in new function
  pushMatrix();
  translate(width, height); //move origin to upper right
  scale( -1, -1); //mirror across origin and make smaller
  displayShapeMatrix( myShapes, rows, cols, cellSize);
  popMatrix();
  
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

///YOU MUST CUSTOMIZE THE LOGIC FOR DESIGN RULES IN THIS FUNCTION
void populate2DArray( PShape[][] shapes, int rows, int cols, float cellSize, color c1, color c2 ) {
  for ( int i=0; i< rows; i++) {
    for ( int j=0; j< cols; j++) {
      int k= i+j; //used for a diagonal pattern
     
     //CUSTOMIZE PATTERN LOGIC
      float fractionk = map( k, 0, rows+cols-2, 0.0, 1.0); //diagonal pattern
      color colorK = lerpColor( c1, c2, fractionk); //diagonal gradient
     
       ///colorAccent MUST BE CHANGED for your project
      color colorAccent = color( 50,100,100); //you must customize, YOU CANNOT USE THIS COLOR
      
      color colorL = lerpColor(colorAccent,c1, fractionk); //concentric color
      
      PShape curShape; //create a variable to refer to PShape
      
      //Combine 2 shapes in 1 region using similar logic
      if ( (k+j) % 3 == 0) { // YOU CANNOT USE THIS EXACT LOGIC - you must customize
        curShape= createPosShape( cellSize  , colorK);    
      } 
      else {
        curShape = createShape(GROUP);
        recursiveShapes( curShape, cellSize *1.6 , 3, colorL);  //make larger than other shape
    
      } //end if-else
      
      shapes[i][j] = curShape; //set the shape as the array element
    }//end inner for-loop - cols
  }//end outer for-loop - rows
}//end function populate2DArray

void recursiveShapes(PShape group,  float len, int level, color c1   ){
  if( level < 1){
    return;
  }
  color curColor = color( hue( c1), saturation(c1), brightness(c1) *.8);
  PShape s = createPosShape( len, curColor);
  group.addChild(s);
  recursiveShapes( group, len *.8, level-1, curColor);
}


PShape customShape1( float len, color c1){
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

