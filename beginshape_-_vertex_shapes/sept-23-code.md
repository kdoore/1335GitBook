#Sept 23 Code:

Final Code for Project 1:

In the code below, I have omitted code for determining how size and color are determined for shapes rendered the positive region of the canvas. Determine the Positive region code ( it is similar to the negative region, except that mouseX will range from balancePoint to width ( mouseX range: 0 ,balancePoint for Negative Region).


```java

float maxLen = 100;
float minLen = 5;
color purplePie;
color aquaTot;
float balancePoint;

void setup( ) {
  size( 1200, 600);
  colorMode(HSB, 360, 100, 100, 100);//HSBA
  background(0);
  //You MUST change these colors to customize your project - change 
  //CHANGE color name and HSB values 
  purplePie = color( 270, 100, 100); //substitute your own colors
  aquaTot = color(180, 100, 100); //substitute your own colors
  balancePoint = width/2; //this is the balancePoint for x dimension
}

void draw( ) {
   if ( mousePressed && frameCount % 10 ==0 ) {
       translate( mouseX, mouseY); //move origin to mouse postion
     if( mouseX < balancePoint){ //NEGATIVE REGION LEFT of Balance Point what do we want to do?
       
        float fraction = map(mouseX ,0 ,balancePoint , 0.0, 1.0); //negative range
        color curColor = lerpColor(purplePie, aquaTot, fraction); //negative range
        float curSize = map( mouseX, 0, balancePoint, maxLen, minLen);
        recursivePattern1( curSize, 5 , curColor);
       
     }//end negative region
       else{ //Right side of the BalancePoint - Positive Region
        //calculate curSize, curColor for Positive region
      /*  complete code statements below
       float curSize = ?
       float fraction = ?
       color curColor = ?
       recursivePattern2( curSize, count?, curColor);
       */
    } //end positive retion
    resetMatrix(); //move origin back to upper left  
   }//end if mousePressed
}//end draw


void recursivePattern1(  float len, int level, color c1    ) {
  if ( level<1) { //termination condition
    return;//stops the function from executing
  }
  //TASK for the recurisve function
  float fraction = map( len, minLen, maxLen, 0.4, 1.0);
  color curColor = color( hue( c1), saturation(c1), brightness(c1) * fraction );
  PShape s1 = createShape1( len, curColor ); //create shape with current len, curColor

  shape( s1, 0, 0); //render the shape on canvas
  
  pushMatrix();
      scale( 1.0, -1.0); //mirror across x axis
      shape( s1, 0, 0); //render the shape on canvas
  popMatrix();
  pushMatrix();
      scale( -1.0, 1.0); //mirror across  y axis
      shape( s1, 0, 0); //render the shape on canvas
  popMatrix();
  recursivePattern1( len * 0.8, level-1, c1);
  
  pushMatrix(); //these are stacked in reverse
      scale( -1.0, -1.0); //mirror across  y axis
      shape( s1, 0, 0); //render the shape on canvas
  popMatrix();
} //end recursivePattern1


//Use in positive region
void recursivePattern2(  float len, int level, color c1    ) {
  if ( level<1) { //termination condition
    return;//stops the function from executing
  }
  //TASK for the recurisve function: very brightness 
  float fraction = map( len, minLen, maxLen, 0.2, 1.0);
  color curColor = color( hue( c1), saturation(c1), brightness(c1) * fraction );
  PShape s1 = createShape2( len, curColor ); //create shape with current len, curColor
  
  ////Let's rotate and render the shape multiple times to create a more complex shape
  pushMatrix();
  float degree=0; 
  while( degree<360){ //test for termination
    rotate( radians( degree));
    shape( s1, 0, 0); //render the shape on canvas
    degree += 180; //lower this value to increase number of rotations
  } //end while
  popMatrix(); 
  
  recursivePattern2( len * 0.8, level-1, c1); //finally the recursive call
  
} //end recursivePattern1



PShape createShape1(  float len, color c1) {
  //fill( c1); //for some PShapes, use fill before creating the shape
  PShape s = createShape() ;
  s.setFill( c1);//for some PShapes, use setFill( ) after creating the shape
  stroke( 40, 30 ); //grayscale, alpha - dark gray, transparent
  s.beginShape();
  s.vertex( 0,0);//point1
  s.vertex(.25*len, .25*len); //pt 2
  s.vertex(.5*len, .25*len); //pt 3
  s.vertex(.5*len, .5*len);  //pt 4
  s.vertex(len, len); ///pt 5
  s.vertex(.5*len, len); //pt 6
  s.vertex(0, .5*len); // pt 7
  s.vertex(0, 0); //pt8
  s.endShape();
  return s;
} //end createShape1


PShape createShape2(  float len, color c1) {
  //fill( c1); //for some PShapes, use fill before creating the shape
  PShape s = createShape() ;
  s.setFill( c1);//for some PShapes, use setFill( ) after creating the shape
  s.beginShape();
  s.vertex( 0,0);//point1
  s.vertex(.25*len, .25*len); //pt 2
  s.vertex(.5*len, .25*len); //pt 3
  s.vertex(.5*len, .5*len);  //pt 4
  s.vertex(len, len); ///pt 5
  //s.vertex(.5*len, len); //pt 6
  s.vertex(0, .5*len); // pt 7
  s.vertex(0, 0); //pt8
  s.endShape();
  return s;
} //end createShape1
```

