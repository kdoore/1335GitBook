Class Code: CS1135.002 Thursday Sept 19






```java
//CS1335_002_Sept19_F19

color purple; //declare the variable
color green, aqua;
float maxLen = 100;
float minLen = 5;
float balancePoint; 

void setup(){
  size( 1000, 600);
  colorMode(HSB, 360, 100, 100, 100); //HSBA
  background(0);
  purple = color ( 280, 100, 100); 
  green = color( 80, 100, 100 );
  aqua = color( 170, 100, 50);
  balancePoint = width/2;
} //end setup

void draw(  ){
if(mousePressed){ //draw a shape if mouse is pressed
    if( mouseX < balancePoint){ //left side: negative side
      translate( mouseX, mouseY); //move the origin to the mouse location
      float fraction =map( mouseX  , 0   , balancePoint  , 0.0   ,  1.0   );
      color curColor = lerpColor(purple, aqua, fraction); 
      float curSize = map(  mouseX,  0   , balancePoint,  maxLen  , minLen );
      recursivePattern1( curSize, 1, curColor );
      resetMatrix();
    }else{ //positive side
      translate( mouseX, mouseY); //move the origin to the mouse location
      recursivePattern1( maxLen, 1, green );
      resetMatrix();
    }
  } //end if
}  //end draw


void recursivePattern1( float len, int level, color c1  ){
  if( level < 1){ //termination conditional test
    return;
   }
  ///task - what is being repeated
  float fraction = map(  len   ,  minLen  , maxLen   , 0.2, 1.0); 
  color curColor = color( hue(c1), saturation(c1), brightness(c1)* fraction);
  PShape curShape = createShape1(  len, curColor );
  shape( curShape, 0, 0);
  recursivePattern1( len * 0.8, level-1, c1); //recursive call
} //end recursivePattern1


PShape createShape1( float len, color c1  ){
 PShape s = createShape();
  s.beginShape();
  s.fill(c1); //HSB - blue full sat, bright
  s.vertex( 0,0); //point 1 for outer shape (clock-wise rotation for drawing points)
  s.vertex(.5* len, .1 * len);  //p2
  s.vertex(.5* len, .5 * len); //p3
  s.vertex(len,  len); //p4
  s.vertex(.5* len,  len); //p5
  s.vertex(0, .5 * len); //p6
  s.vertex(.25* len, .25 * len); //p7
  s.vertex( 0,0); //last point for outer shape
  s.endShape(CLOSE); //end shape
  
  return s;
} //end createShape1
```

