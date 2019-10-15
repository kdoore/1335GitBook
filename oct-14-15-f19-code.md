#Recursive Pattern with Group-type PShape

```java
void setup() {
  size( 1200, 1200);
  colorMode(HSB, 360, 100, 100);
  background(0);
  color purple = color( 280, 100, 100);
  color aqua = color(180, 100, 100);
  
  int rows = 20;
  int cols = 20;
  
  float cellSize = width/cols;
  PShape[][] myShapes = new PShape[rows][cols]; //num elements is rows*cols
  populate2DArray( myShapes, rows, cols, cellSize, purple, aqua);

  //display in region1 at smaller (1/4) scale
  pushMatrix();
  scale( 0.5, 0.5);
  displayShapeMatrix( myShapes, rows, cols, cellSize);
  popMatrix();
 
  //region2
  
  mirrorRegion2( myShapes, rows, cols, cellSize);
  

  //region3
  pushMatrix();
  translate(0, height); //move origin to upper right
  scale( 0.5, -0.5); //mirror across x-axix, make smaller
  displayShapeMatrix( myShapes, rows, cols, cellSize);
  popMatrix();



  //region4
   pushMatrix();
  translate(width, height); //move origin to upper right
  scale( -0.5, -0.5); //mirror across origin and make smaller
  displayShapeMatrix( myShapes, rows, cols, cellSize);
  popMatrix();
}

void mirrorRegion2( PShape[][] shapes, int rows, int cols, float cellSize  ){
  //region2
  pushMatrix();
  translate(width, 0); //move origin to upper right
  scale( -0.5, 0.5); //mirror and scale smaller 
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
          //curShape= createShape1(cellSize, colorK); //rect if k is even
          curShape = createShape(GROUP);
          recursivePattern1( curShape, cellSize, 3, colorK);
      } else {
        fill(colorL);
        curShape= createShape(ELLIPSE, 0, 0, cellSize, cellSize); //rect if k is even
      } //end if-else
      shapes[i][j] = curShape; //set the shape as the array element
    }//end inner for-loop - cols
  }//end outer for-loop - rows
}//end function populate2DArray


PShape createShape1( float len, color c1){
  PShape s = createShape( RECT, 0,0, len, len);
  s.setFill( c1);
  return s;
}
///PShape g must be a group PShape, we'll add each recursive PShape as a child
void recursivePattern1( PShape g, float len, int level, color c1    ){
  if( level < 0){
    return;
  }
  color curColor= color( hue( c1), saturation( c1), brightness(c1) *.8);
  PShape childShape = createShape1( len, curColor);
  g.addChild( childShape);
  recursivePattern1(  g,len * .8, level-1, curColor);
}
```

