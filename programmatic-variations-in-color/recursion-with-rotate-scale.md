#Recursion with Rotate, Scale

Using Rotate or Scale( ) within the Recursive Function allows for creating complex shapes using rotation and mirroring.

![](/assets/Screen Shot 2019-09-22 at 7.42.20 PM.png)


```java

float maxLen, minLen;
color cNeg1, cNeg2, cNegPop1, cNegPop2;
color cPos1, cPos2, cPosPop1, cPosPop2;

void setup(){
size( 1000, 1000);
colorMode(HSB, 360, 100, 100, 100);
background(0);
maxLen = 50;
minLen=1;
cNeg1 = color( 285, 100,100); //purple
cNeg2 = color( 260, 100, 100); //blue
cPos1 = color( 185, 100,100); //aqua
cPos2 = color( 230, 100, 100);//blue
}

void draw(){
    if(mousePressed && frameCount %5 == 0){
    translate( mouseX, mouseY);
    float dist = dist( mouseX, mouseY, width/2, height/2);
    if( mouseX < width/2 ){
    //determine how color, size change across Negative region
        float curLen = map( mouseX, 0, width/2, maxLen, minLen);
        float lerpFraction = map( mouseX, 0, width/2, 0.0, 1.0);
        color curColor = lerpColor( cNeg1, cNeg2, lerpFraction);
        
        recursivePattern1( curLen, 5, curColor);
    
    }//end negative region
    else if( mouseX > width/2 ){ //positive region

    //create similar code for positive region

    } //end if positive region
    resetMatrix();
    } //end if mousePressed
} //end draw

void recursivePattern1(float len, float level, color c1){
if( level<1){
return;
}
color shapeColor = color( hue(c1), saturation(c1), brightness(c1)*.8 );
PShape s= createNegShape( len, c1);

shape( s, 0,0); //render shape to canvas

pushMatrix();
    scale( -1.0, 1.0); //mirror across y-axis
    shape( s,0, 0);//render shape to canvas
popMatrix();

pushMatrix();
    scale( 1.0, -1.0);//mirror across x-axis
    shape( s,0, 0);//render shape to canvas
popMatrix();

recursivePattern1( len * .8, level-1, shapeColor);

pushMatrix();
    scale( -1.0, -1.0); //mirror across x,y axis
    shape( s,0, 0); //rendered after recursive call, reversed stack order
popMatrix();
}

void recursivePattern2(float len, float level, color c1){
if( level<1){
return;
}
color shapeColor = color( hue(c1), saturation(c1), brightness(c1)*.8 );
PShape s= createPosShape( len, c1);
float degrees=0;
pushMatrix();
while( degrees< 360){
rotate( radians( degrees));
shape( s, 0,0);
degrees += 45;
}
popMatrix();
recursivePattern2( len * .8, level-1, shapeColor);
} //end recursivePattern2

PShape createNegShape(float len, color c1){
PShape s = createShape();
s.setFill( c1);
s.beginShape();
stroke( 30,40);
s.vertex(0,0 ); //1
s.vertex(.2*len,.1*len ); //2
s.vertex(.3*len,0 ); //3
s.vertex(.7*len,0 ); //4
s.vertex(.8*len,.1*len); //5
s.vertex(1.0*len,.1*len); //6
s.vertex(1.1*len,.2*len ); //7
s.vertex(1.0*len,.3*len ); //8
s.vertex(1.1*len,.4*len ); //9
s.vertex(1.1*len,.5*len); //10
s.vertex(1.2*len,.6*len); //11
s.vertex(1.2*len,.7*len); //12
s.vertex(1.1*len,.8*len); //13
s.vertex(.9*len,.7*len); //14
s.vertex(1.0*len,.9*len); //15
s.vertex(.9*len,1.0*len); //16
s.vertex(.8*len,.9*len); //17
s.vertex(.4*len,.9*len); //18
s.vertex(.3*len,1.0*len); //19
s.vertex(.1*len,.8*len); //20
s.vertex(.2*len,.7*len); //21
s.vertex(.2*len,.6*len); //22
s.vertex(.1*len,.5*len); //23
s.vertex(.1*len,.4*len); //24
s.vertex(0*len,.3*len); //25
s.vertex(.1*len,.2*len); //26
s.vertex(0*len,0*len); //back to first point
s.beginContour();
s.vertex(.3*len,.3*len ); //1
s.vertex(.3*len,.4*len); //15
s.vertex(.4*len,.5*len); //14
s.vertex(.4*len,.7*len); //13
s.vertex(.5*len,.8*len); //12
s.vertex(.7*len,.8*len); //11
s.vertex(.7*len,.7*len); //10
s.vertex(.8*len,.7*len ); //9
s.vertex(.9*len,.6*len ); //8
s.vertex(.8*len,.5*len ); //7
s.vertex(.9*len,.4*len); //6
s.vertex(.8*len,.3*len); //5
s.vertex(.7*len,.3*len ); //4
s.vertex(.6*len,.2*len ); //3
s.vertex(.4*len,.2*len ); //2
s.vertex(.3*len,.3*len ); //1
s.endContour();
s.endShape(CLOSE);
return s;
}

PShape createPosShape(float len, color c1){
PShape s = createShape();
s.setFill( c1);
s.beginShape();
//s.noStroke();
stroke( 30,20);
s.vertex(0,0 ); //1
s.vertex(.1*len,.1*len ); //2
s.vertex(.3*len,.2*len ); //3
s.vertex(.3*len,.3*len ); //4
s.vertex(.5*len,.4*len); //5
s.vertex(.5*len,.5*len); //6
s.vertex(.7*len,.6*len ); //7
s.vertex(.7*len,.7*len ); //8
s.vertex(.9*len,.8*len ); //9
s.vertex(1.0*len,1.0*len); //10
s.vertex(.8*len,.9*len); //11
s.vertex(.7*len,.8*len); //12
s.vertex(.6*len,.9*len); //13
s.vertex(.6*len,.7*len); //14
s.vertex(.5*len,.6*len); //15
s.vertex(.4*len,.6*len ); //16
s.vertex(.4*len,.7*len ); //17
s.vertex(.5*len,.8*len ); //18
s.vertex(.5*len,1.0*len ); //19
s.vertex(.4*len,.8*len); //20
s.vertex(.3*len,.7*len); //21
s.vertex(.3*len,.6*len ); //22
s.vertex(.4*len,.5*len ); //23
s.vertex(.3*len,.4*len ); //24
s.vertex(.2*len,.4*len); //25
s.vertex(.3*len,.5*len); //26
s.vertex(.2*len,.5*len); //27
s.vertex(.2*len,.7*len); //28
s.vertex(.1*len,.5*len); //29
s.vertex(.1*len,.4*len); //30
s.vertex(.2*len,.3*len); //31
s.vertex(.1*len,.4*len); //32
s.vertex(0,0 ); //1 //back to first point
s.endShape(CLOSE);
return s;
}


```

