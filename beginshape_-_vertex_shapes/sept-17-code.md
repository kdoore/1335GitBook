#CS1335.002 Tues Sept 17 Class Code - Project 1

```java

//CS1335_002_Sept17_F19

color purple; //declare the variable
color green;
float maxLen = 100;
float minLen = 5;

void setup(){
  size( 1000, 600);
  colorMode(HSB, 360, 100, 100, 100); //HSBA
  purple = color ( 280, 100, 100); 
  green = color( 80, 100, 100 );
} //end setup

void draw(  ){
  
  if(mousePressed){ //draw a shape if mouse is pressed
    translate( mouseX, mouseY); //move the origin to the mouse location
  
     recursivePattern1( maxLen, 10, purple );
  
    resetMatrix();
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
  //fill(c1);   //remember fill can be a problem, this might be the right way to set fill
  PShape s = createShape( RECT, 0,0,len, len);
  s.setFill( c1);
  return s;
} //end createShape1
```

