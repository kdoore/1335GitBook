#March 13, S19 Code

```java 

void setup() {
  size( 600, 600);
  colorMode(HSB, 360, 100, 100);
  background(0);
  color c1 = color( 270, 100, 50);//dark purple
  color c2 = color( 180, 100, 100); //cyan
  color c4 = color( 0, 100, 100  ); //red -some other color
  int rows = 20;
  int cols = 20;
  int size = width/cols;
  //data-type, variable name, initialize: objects: use 'new'
  PShape[][] shapeMatrix = PopulateGradientGrid(   rows, cols,   size,   c1,  c2);

  DisplayShapeMatrix( shapeMatrix, 0, 0, rows,  cols, size);
  
} //end setup


void DisplayShapeMatrix(PShape[][] shapes, int x, int y, int rows, int cols, float size){
  pushMatrix();
  translate( x, y);
  
  int xPos=0;  //for creating grid layout
  int yPos=0;  //for creating grid layout

  //nested for-loops -here we are populating and displaying at the same time
  for ( int i=0; i< rows; i++) {
    for ( int j=0; j< cols; j++) { 
     shape( shapes[i][j], xPos, yPos);
      xPos += size;
    } //end inner for-lop 
    xPos = 0; //reset at end of each row
    yPos += size; //reset for moving down to next row
  }//end outer for-loop
  popMatrix();
}//end function



PShape[][] PopulateGradientGrid( int rows, int cols, float size, color c1, color c2) {
  PShape[][] shapes = new PShape[rows][cols];
  for ( int i=0; i< rows; i++) {
    for ( int j=0; j< cols; j++) {
      int k = i + j;  ///play with this logic to determine k
      int l = min( i, j);

      float fractionk = map( k, 0, rows-1 + cols -1, 0.0, 1.0);  //want full range for lerpColor
      float fractionl = map( l, 0, rows-1, 0.0, 1.0); //want full range of colors

      color c3 = lerpColor( c1, c2, fractionk);
      color c5 = lerpColor( color( 0), c1, fractionl);

      PShape curShape;
      if ( k % 2 == 0 ) {  //k is even number

        fill( c3); //color set by k logic
        curShape = createShape(RECT, 0, 0, size * .9, size * .9);
      } //end if
      else {

        fill( c5); //color set by l logic
        curShape = createShape(ELLIPSE, (size/2), (size/2), size * .9, size * .9);
      } //end else
      shapes[i][j] = curShape;
    } //end inner for-lop
  }//end outer for-loop
  return shapes;
}

```

