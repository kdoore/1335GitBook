In class code for Monday Feb 4, Wed Feb 6, 2019

```java
float lenMin, lenMax;

void setup(){
  size( 600, 600);
  colorMode(HSB, 360, 100, 100, 100);
  background(0);
  rectMode( CENTER);
  lenMin = 5;
  lenMax = 100;
  
}



void draw(){
  if(mousePressed  ){
    
    //left region
    float fraction;
    float dimension;
    color c1 = color( 182, 100, 100); //cyan
    color c2 = color( 84, 100, 100); //.lime
    color c4 = color( 40, 100,80); ////orange
    color c5 = color(280, 100, 100 ); // purple
    
    translate( mouseX, mouseY);
    if( mouseX < width/2){
     dimension = map( mouseX, 0, width/2, lenMax, lenMin);
     fraction = map( mouseX, 0, width/2, 1.0, 0.0);
     color c3 = lerpColor( c1, c2, fraction); //changes as mouseX changes
     pattern1( dimension, c3);
    }
    else{   //right region
     dimension = map( mouseX,  width/2, width, lenMin, lenMax);
     fraction = map( mouseX,  width/2, width, 0.0, 1.0);  
     color c6 = lerpColor( c4, c5, fraction); //changes- orange to purple as mouseX changes
     pattern2( dimension, c6);
    } //end if-else
    resetMatrix();
  } 
  
}//end draw



void pattern1(float len, color c1 ){
  
  PShape s = shape1( len, c1);
  shape( s, 0, 0);
}


void pattern2( float len,  color c1){
  PShape s = shape2( len, c1);
  shape( s, 0, 0);
  
}

//creates a single shape 
PShape shape1( float len, color c1){
  fill( c1);
  PShape s = createShape( RECT, 0,0, len, len);
  return s;
}


//creates a single shape 
PShape shape2( float len, color c1){
  fill( c1);
  PShape s = createShape( ELLIPSE, 0,0, len, len);
  return s;
}





```

