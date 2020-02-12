Class Code Feb12 Spring 2020

```java
//Feb 12, 2020
float maxSize = 100;
float minSize = 30;
void setup(){
  size( 600, 600);
  colorMode(HSB, 360, 100, 100, 100);//HSBA
}
 
 void draw(){
  //select 2 colors for positive region
  color c1Pos = color( 280, 100, 100);//purple
  color c2Pos = color(80, 100, 100);//
  
  if(mousePressed){
     translate( mouseX, mouseY); //move origin to mouse position
     posRecursivePattern( maxSize, 5,c1Pos, c2Pos);
     resetMatrix();
  }
   
 }
 
 
 //repeat of a shape with varying size and color
 void posRecursivePattern(float size,  int count, color c1, color c2  ){
   if( count <0){ //test for termination
     return; //end function execution
   }
   
   float fraction = map( size, minSize, maxSize, 0.0, 1.0);
   color c3 = lerpColor( c1, c2, fraction); //0, c1....1, c2 
   PShape s1 = customPosShape(size, c3 );  //create our shape
   shape( s1, 0,0); //render the shape to the canvas
 
   posRecursivePattern(size*0.8, count-1, c1, c2 );
 }
 
//function to create a custom shape
PShape customPosShape( float len, color cfground ){
  PShape s; //declare our first object-type variable //heap - object memory
  fill( cfground);//attempt to set color for the shape
  s = createShape( );//initialize our shape
  s.beginShape();
  s.vertex( 0,0  ); //1 x, y points
  s.vertex(.5 * len , 0 ); //2
  s.vertex(len , .5* len ); //3
  s.vertex(.5 * len , len  );//4
  s.vertex( 0,  .5* len ); //5
  s.vertex( 0, 0 ); //6
  
  
  s.beginContour(); //make internal cutout 
  s.vertex( len*.25,len*.45); //inner cutouts - point 5
  s.vertex(len*.6, len*.6);  // 
  s.vertex( len*.45, len*.25); // 
  s.vertex(0,0);
  s.endContour(); //end internal cutout

  
  s.endShape();
  //shape( s, 0,0);  //render to the canvas
  return s; //return the PShape
}


```


  