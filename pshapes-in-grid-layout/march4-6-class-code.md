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

