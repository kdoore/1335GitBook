Sept - 18
Class Code:  

```java

float maxLen = 100;
color purple;
color green;
color aqua;
float balancePoint;

void setup( ) {
  size( 1200, 600);
  colorMode(HSB, 360, 100, 100, 100);//HSBA
  background(360);
  purple = color( 270, 100, 100);
  green = color( 80, 100, 100);
  aqua = color(180, 100, 100);
  balancePoint = width/2; //this is the balancePoint for x dimension
}

void draw( ) {
   if ( mousePressed) {
     if( mouseX < balancePoint){ //LEFT of Balance Point what do we want to do?
        translate( mouseX, mouseY); //move origin to mouse postion
        float fraction = map(mouseX ,0 ,balancePoint , 0.0, 1.0);
        color curColor = lerpColor(purple, aqua, fraction);
        recursivePattern1( maxLen, 5, curColor);
        resetMatrix(); //move origin back to upper left
       }
       else{ //Right side of the BalancePoint
        translate( mouseX, mouseY); //move origin to mouse postion
        recursivePattern1( maxLen, 5, green);
        resetMatrix(); //move origin back to upper left  
       }
   
  }//end if mousePressed
}//end draw


void recursivePattern1(  float len, int level, color c1    ) {
  if ( level<1) { //termination condition
    return;//stops the function from executing
  }
  //TASK for the recurisve function
  float fraction = map( len, 0, maxLen, 0.4, 1.0);
  color curColor = color( hue( c1), saturation(c1), brightness(c1) * fraction );
  PShape s1 = createShape1( len, curColor ); //create shape with current len, curColor

  shape( s1, 0, 0); //render the shape on canvas
  pushMatrix();
      scale( -1.0, -1.0); //mirror across x, y axis
      shape( s1, 0, 0); //render the shape on canvas
  popMatrix();
  
  recursivePattern1( len * 0.8, level-1, c1);

} //end recursivePattern1


PShape createShape1(  float len, color c1) {
  //fill( c1); //for some PShapes, use fill before creating the shape
  PShape s = createShape() ;
  s.setFill( c1);//for some PShapes, use setFill( ) after creating the shape
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
```

