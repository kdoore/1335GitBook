#Class Code - March 4,,6


###Class Code March 4
```java

void setup(){
  size( 600, 600);
  colorMode(HSB, 360, 100, 100);
  int rows = 10;
  int cols = 10;
  float cellSize = width / cols; //how big is each cell
  color c1 = color( 270, 100, 50); //dark purple
  color c2 = color( 180, 100, 100); //cyan
  //check that we can create and display a single shape
  //PShape s1 = createShape1( cellSize, c1); //make 1 PShape
  //shape(s1, 200, 200); //display 1 shape
  PShape[] shapes; //declare the array
  shapes = new PShape[ rows * cols ];  //100 
  println(shapes[0] == null);//true - shapes[0] has not been initialized
  PopulateShapeList( shapes, cellSize, c1, c2);
  println(shapes[0]== null);//should be false if shapes[0] does contain a PShape
  shape( shapes[99], 200, 200); //display one of these
}

void displayShapeMatrix(PShape[] shapes,  float cellSize, int rows, int cols    ){
  
  for( int i=0; i< rows; i++){
    for( int j=0; j< cols; j++){
    
    } //end inner loop
   } //end outer loop
}

void PopulateShapeList(PShape[] shapes,float cellSize, color c1, color c2  ){
  int count = shapes.length;
  //use a for-loop to populate each array element with 1 PShape
  for( int i=0; i < count; i++){
    shapes[i] = createShape1( cellSize, c1);
  } //end for-loop
  
} //end function


PShape createShape1( float len, color c1){
  PShape s = createShape( RECT, 0,0, len, len);
  s.setFill( c1); //OOP - setFill is a method to set fill for a PShape
  return s;
}
```
###Complete Code - March 6
We complete the DisplayShapeMatrix, and create a design with Parametric variation logic in the PopulateShapeList function.

When creating each shape, in PopulateShapeList, we can create variation for the custom shape by varying values supplied as parameters for the createShape1( float len, color c1).   To do this, we create 2 variables: float len, color c3.  These values are calculated using the map function and colorLerp function.  This logic must be within the for-loop that's creating each shape.  Within the for-loop, we have the loop-control variable:  i, which changes from 0, count-1.  So we use this changing value to calculate changing values for len, c3, which are used as parameters for the createShape1 function.

However, we're limited to linear changes in our pattern, since we're using changing values of i, and i changes in a linear way.  When we switch to 2D arrays for storing our data, then we can use more complex logic to create more sophisticated color / shape patterns in our data.

![](/assets/Screen Shot 2019-03-06 at 11.44.50 AM.png)
```

void setup(){
  size( 600, 600);
  colorMode(HSB, 360, 100, 100);
  background(0);
  int rows = 10;
  int cols = 10;
  float cellSize = width / cols; //how big is each cell
  color c1 = color( 270, 100, 50); //dark purple
  color c2 = color( 180, 100, 100); //cyan
  //check that we can create and display a single shape
  //PShape s1 = createShape1( cellSize, c1); //make 1 PShape
  //shape(s1, 200, 200); //display 1 shape
  PShape[] myShapes; //declare the array
  myShapes = new PShape[ rows * cols ];  //100 
  //println(myShapes[0] == null);//true - shapes[0] has not been initialized
  PopulateShapeList( myShapes, cellSize, c1, c2);
  //println(myShapes[0]== null);//should be false if shapes[0] does contain a PShape
  //shape( myShapes[99], 200, 200); //display one of these
  displayShapeMatrix( myShapes, cellSize, rows, cols );
}

void displayShapeMatrix(PShape[] shapes,  float cellSize, int rows, int cols    ){
  int k=0; //index to track which shapes[k] item to display
  //shape( shapes[k], xPos, yPos) //to draw 1 shape
  float xPos = 0; ///where do we draw each shape
  float yPos = 0;
  for( int i=0; i< rows; i++){
    for( int j=0; j< cols; j++){
        shape( shapes[k], xPos, yPos);
        xPos += cellSize; //move xPos over to next cell each time loop executes
        k++; ///REMEMBER THIS - k determines which array item to display
  } //end inner loop - j determines cols
   xPos = 0; //reset to 0 for the next row to start at the left edge
   yPos += cellSize;
  
 } //end outer loop - i determines rows
}

void PopulateShapeList(PShape[] shapes,float cellSize, color c1, color c2  ){
  int count = shapes.length;
  //use a for-loop to populate each array element with 1 PShape
  for( int i=0; i < count; i++){
    //make customizations for parametric design 
    //use i, which changes between 0, count-1, to create parametric variation
    float fraction = map( i, 0, count-1,0.0, 1.0); //use for lerp color
    //println("fraction " + fraction);
    color c3 = lerpColor( c1, c2, fraction);
    //println("hue " + hue( c3));
    float fraction2 = map( i, 0, count-1,0.5, 1.0); //use to vary len
    float len = cellSize * fraction2;
    shapes[i] = createShape1( len,c3);
  } //end for-loop
  
} //end function

PShape createShape1( float len, color c1){
  PShape s = createShape( RECT, 0,0, len, len);
  s.setFill( c1); //OOP - setFill is a method to set fill for a PShape
  return s;
}


```
In the example below, the number of rows, cols has been set to 50 in setup.


```java
 int rows = 50;
 int cols = 50;
```


![](/assets/Screen Shot 2019-03-06 at 11.45.15 AM.png)