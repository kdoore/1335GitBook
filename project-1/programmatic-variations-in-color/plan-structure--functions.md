---
description: Plan structure of functions for Positive and Negative Regions
---

# Planning Structure: Functions:

#### Define Global Variables

* Define global variables to determine size range for pattern
* Define global variable balancePoint - can be animated for more interest 

#### Define Positive, Negative Custom Shape Functions

* Define custom Shape functions:
* Creates a single shape using len, c1

  * posCustomShape\( float len, color c1\)
  * negCustomShape\( float len, color c1\)

#### Define  Positive, Negative RecursivePattern Functions

* Define recursive functions: Creates a set of nested shapes - gradient in size, brightness
* Include Logic to determine changing brightness, changing size for each layered shape.

  * posRecursivePattern\( float len, color c1, color c2\)
  * negRecursivePattern\( float len, color c1, color c2\)

#### Define Positive, Negative Pattern Functions

* Define functions:  Creates 1 pattern - at  current mouse position, Gradients in color and size across the positive region
  * positivePattern\( float balancePoint \)
  * negativePattern\( float balancePoint\)

Example Code

```java

float balancePoint;
float minSize = 1;
float maxSize = 50;

void setup(){
  size( 600, 600);
  colorMode(HSB, 360, 100, 100, 100);//HSBA
  background(0);
  balancePoint = width/2;
}
 
 void draw(){
  
  if(mousePressed){
     translate( mouseX, mouseY); //move origin to mouse position
        if( mouseX > balancePoint){
        positivePattern( balancePoint);
        }
        else{
        //negPattern(balancePoint);
        }
    resetMatrix();
  }
   
 }
 
 void positivePattern( float balancePoint){
   color c1 = color( 80, 100, 100);
   color c2 = color ( 280, 100, 100);
   float lenMax = 100;
   float lenMin = 10;
    //determine curColor, curSize
   float fraction = map( mouseX, balancePoint, width, 0.0, 1.0);
   color curColor = lerpColor( c1, c2, fraction);
   float curSize = map( mouseX, balancePoint, width, lenMin, lenMax);
   posRecursivePattern( curSize, curColor);
 }
 
 //repeat of a shape with varying size and color
 void posRecursivePattern(float size, color c1){
   if( size <minSize){ //test for termination
     return; //end function execution
   }
   //determine brightness
   float fraction = map( size, minSize, maxSize, 0.5, 1.0);
   color curColor = color( hue(c1), saturation(c1), brightness(c1) * fraction);
   
   PShape s1 = customPosShape(size, curColor );  //create our shape
   shape( s1, 0,0); //render the shape to the canvas
 
   posRecursivePattern(size*0.8,  c1  );
   //Create 2nd shape flipped across the origin
   //shapes stacked in reverse order
   pushMatrix();
   scale( -1, -1);
   shape( s1, 0,0);
   popMatrix();
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

