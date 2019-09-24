#Sept 24 Code

Final Code for Project 1:

In the code below, I have omitted code to setup the positive region's gradients for size and color for shapes rendered the positive region. 

You must determine the code for Positive region. ( it is similar to the negative region, except that mouseX will range from balancePoint to width ( mouseX range: 0 ,balancePoint for Negative Region).

You must define different colors than the ones used in the code below

```java


//CS1335_002_Sept19_F19

color purplePie; //declare the variable
color greenGoo, aquaTot;
float maxLen = 150;
float minLen = 5;
float balancePoint; 

void setup(){
  size( 1400, 1000);
  colorMode(HSB, 360, 100, 100, 100); //HSBA
  background(0);
  purplePie = color ( 281, 100, 100); 
  greenGoo = color( 131, 100, 100 );
  aquaTot = color( 171, 100, 50);
  balancePoint = width/2;
} //end setup

void draw(  ){
if(mousePressed  && frameCount%10 == 0 ){ //draw a shape if mouse is pressed
 translate( mouseX, mouseY); //move the origin to the mouse location
  ///LOGIC FOR EACH REGION: COLOR CHANGE AND SHAPE, SIZE CHANGE
    if( mouseX < balancePoint){ //left side: negative side
     
      float fraction =map( mouseX  , 0   , balancePoint  , 0.0   ,  1.0   );
      color curColor = lerpColor(purplePie, aquaTot, fraction); 
      float curSize = map(  mouseX,  0   , balancePoint,  maxLen  , minLen );
      float randDegree = random(0, 17); //randomly rotate before drawing each motif
      rotate( radians( randDegree));
      recursivePattern1( curSize, 5, curColor );
    }
    
    else{ //Add code for varying color, shape, size in positive range
    //similar to negative range except mouseX goes from balancePoint to width in Positive Range
       
      //recursivePattern2( curSize, 5, curColor );
      
    }
    
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
  
  pushMatrix();
      scale( -1.0, 1.0);  //flip across y-axis
      shape( curShape, 0, 0);
  popMatrix();
  
  //add code to flip across x-axis using scale transform if desired
  
  recursivePattern1( len * 0.8, level-1, c1); //recursive call
  //task after recursive call means it is stacked and executed in reverse order
  //asymmetric due to reverse stacking:  largest, brightest shape drawn last
   //add code here to flip across xy-axis using scale transform if desired
  
} //end recursivePattern1



PShape createShape1( float len, color c1  ){
 PShape s = createShape();
  s.beginShape();
  s.fill(c1); //HSB - blue full sat, bright
  s.vertex( 0,0); //point 1 for outer shape (clock-wise rotation for drawing points)
  s.vertex(.5* len, .1 * len);  //p2
  s.vertex(.5* len, .5 * len); //p3
  //s.vertex(len,  len); //p4
  s.vertex(.5* len,  len); //p5
  s.vertex(0, .5 * len); //p6
  s.vertex(.25* len, .25 * len); //p7
  s.vertex( 0,0); //last point for outer shape
  s.endShape(CLOSE); //end shape
  
  return s;
} //end createShape1


```

