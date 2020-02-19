# Final Example Code

```java
float minSize, maxSize;
float balancePoint;

void setup(){
  size( 1200, 1200);
  colorMode( HSB, 360, 100, 100,100);
  background(0);//only set one time
  minSize = 10;
  maxSize = 60;
  balancePoint = width/2;  //start at middle of canvas
}

void draw(){
  if(mousePressed && frameCount%5 ==0 ){ //timer only draw pattern every 10 frames
    translate( mouseX, mouseY);//translate origin to mouse position
    if( mouseX > balancePoint){
     positivePattern( balancePoint, mouseX);
    }
    else{
     negativePattern(  balancePoint, mouseX);
    }
  
    resetMatrix();
  } //end if-mousePressed
  
}//end of draw

void negativePattern( float balancePoint, int mX){
    //TODO  Add logic here for changing color, size across negative region
    //call negRecursivePattern(  curSize, curColor);
}

//determine current size, color: gradients across the positive region
void positivePattern(  float balancePoint, int mX){
   ///positive region colors
  color cPos1 = color( 230, 100, 100); //purple
  color cPos2 = color( 80, 100, 100); //lime
  color randPop = color( 55, 100, 100);//yellow
  
  //define curColor based on mX relative to balancePoint
  float fraction = map( mX, balancePoint, width, 0.0, 1.0);
  color curColor = lerpColor( cPos2, cPos1, fraction); //fraction varies beteween 0.0, 1.0
  
  float rand = random( 0.0, 1.0); //flip a coin 
  
  if( rand< 0.2){
    curColor = randPop;  //use random pop of color 
  }
  float curSize = map( mX, balancePoint, width, minSize, maxSize );
  
  pushMatrix();
  float randAngle = random( -90.0, 90.0);
  rotate( radians(randAngle)); 
  posRecursivePattern( curSize, curColor); //creates 1 motif
  popMatrix();
}

void negRecursivePattern( float size, color c1){
  //termination test
  
  //task
  
  //recursive call with size changing: converging toward termination
}


//Draws a single motif - nested size and color gradient
void posRecursivePattern( float size, color c1){
  //termination test
  if(size < minSize){
    return;
  }
  //task
  float fraction = map( size, minSize, maxSize, 0.2, 1.0); //may want to customize
  color curColor = color( hue(c1), saturation( c1), brightness(c1)*fraction);
  
  PShape s1 = customPosShape( size, curColor); //test the shape
  
  shape(s1,0,0); //task1:render the shape at the origin
  
  pushMatrix();
  scale( -1, 1);   //task2: mirrored across the y axis
  shape( s1, 0, 0);
  popMatrix();
  
  pushMatrix();
  scale( 1, -1);   //task3: mirrored across the x axis
  shape( s1, 0, 0);
  popMatrix();
  
  //recursive call
  posRecursivePattern( size * 0.8, c1); //modify size so we terminate
  
  //task 4 - with reversed stacking - mirror across origin
  pushMatrix();
  scale( -1, -1);//mirror across the x, y axis (origin)
  shape( s1, 0, 0);
  popMatrix();
}

PShape customNegShape( float len, color c1){
  fill( c1);
  PShape s = createShape( RECT, 0,0, len, len);//placeholder shape
  
  return s;
}

//Draws a single shape
PShape customPosShape(  float len, color c1){
  PShape s; //declare our first object-type variable //heap - object memory
  fill( c1);//attempt to set color for the shape
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

