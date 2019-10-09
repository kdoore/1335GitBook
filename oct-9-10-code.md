###Oct 9, 10 F19 
In Class Code


```java

void setup(){
  size( 600, 600);
  colorMode(HSB, 360, 100, 100);
  background(0);
  color purple = color( 280, 100, 100);
  color aqua = color(180, 100, 100);
  int rows = 20;
  int cols = 20;
  float cellSize = width/cols;
  
  PShape[][] myShapes = new PShape[rows][cols]; //num elements is rows*cols
  populate2DArray( myShapes, rows, cols, cellSize, purple, aqua);
  
  //shape( myShapes[0][0], 0,0); //display one shape
  pushMatrix();
  scale( 0.5,0.5);
  displayShapeMatrix( myShapes, rows, cols, cellSize);
  popMatrix();
  
  
  pushMatrix();
  translate(width, 0); //move origin to upper right
  rotate( radians(90));
  scale( 0.5,0.5);
  displayShapeMatrix( myShapes, rows, cols, cellSize);
  popMatrix();
  
  
  pushMatrix();
  translate(0, height); //move origin to upper right
  rotate( radians(270));
  scale( 0.5,0.5);
  displayShapeMatrix( myShapes, rows, cols, cellSize);
  popMatrix();
  
  pushMatrix();
  translate(width, height); //move origin to upper right
  rotate( radians(180));
  scale( 0.5,0.5);
  displayShapeMatrix( myShapes, rows, cols, cellSize);
  popMatrix();
}


void displayShapeMatrix( PShape[][] shapes, int rows, int cols, float cellSize   ){
  int xPos=0; 
  int yPos=0;
  
  for( int i=0; i< rows; i++){
    for( int j=0; j< cols; j++){
       shape(  shapes[i][j],xPos, yPos); //display one shape           
       xPos += cellSize;
     }//end inner loop - cols
  xPos = 0;  //reset xPos to 0 for next row
  yPos += cellSize;
} //end outer loop - rows

}//end function


void populate2DArray( PShape[][] shapes, int rows, int cols, float cellSize, color c1, color c2 ){
  for( int i=0; i< rows; i++){
    for( int j=0; j< cols; j++){
      int k= i+j;  //used for a diagonal pattern
      int l= min( i,j); //concentric pattern
      float fractionk = map( k, 0,rows+cols-2, 0.0, 1.0); 
      float fractionl= map( l,0, rows-1, 0.0, 1.0);
       //use fractions to create color gradient patterns
      color colorK = lerpColor( c1, c2, fractionk); //diagonal gradient
      color colorL = lerpColor(color(0),c1, fractionl); //concentric color
      
      PShape curShape;    //create a shape
      if( k%2==0){
        fill( colorK);
        curShape= createShape(RECT, 0,0,cellSize, cellSize);  //rect if k is even
       }else{
         fill(colorL);
         curShape= createShape(ELLIPSE, 0,0,cellSize, cellSize);  //rect if k is even
      } //end if-else
      shapes[i][j] = curShape;  //set the shape as the array element
    }//end inner for-loop - cols
   }//end outer for-loop - rows
}//end function populate2DArray


```

