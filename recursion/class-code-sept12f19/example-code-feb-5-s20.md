Example Class Code: Feb 5, 2020

Introduction to Recursion 



```java
//Feb 5, 2020
  
  
float maxSize = 300; //global variable

void setup(){
  size( 600, 600);
  colorMode(HSB, 360, 100, 100, 100);//HSBA
  
  //drawCircle( width/2, height/2,  300);
  drawRecursiveCircles(  width/2, height/2, maxSize, 10); //call recursive function
 }

//Recursive function - repeat structure to repeat some task
//Recursive function calls itself within the function body
//Recursive function requires termination test before recursive call
  
void drawRecursiveCircles(float x, float y, float size,  int count  ){
  if( count <0){  //stop repeat - test for termination
    return; //stops execution of the function
  }
  count--;  //decrease our count variable
  float hue = map( size, 0, maxSize, 0, 90);
  fill( hue, 100, 100,30);
  ellipse( x, y, size, size); //task
  drawRecursiveCircles(x+ size * 0.8  , y, size * 0.8, count );  //recursive call:  call the function itself
  drawRecursiveCircles(x- size * 0.8  , y, size * 0.8, count );  //recursive call:  call the function itself
}

void drawCircle( float x, float y, float size){
  //termination condition - RED FLAG
  for( int i= 1 ; i< 10; i++){
  ellipse( x, y, size/i, size/i); //draw a single ellipse
  }
  
}
```

