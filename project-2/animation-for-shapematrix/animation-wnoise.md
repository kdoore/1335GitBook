# Animation w/Noise

Animation with noise( ) added to the animation timer gives more organic feeling of energy. ![](http://g.recordit.co/PQa5TfBSiv.gif)

Similar animation without noise has perfectly consistant timing. ![](http://g.recordit.co/kE4Jf0tdPT.gif)

#### noise(  ) &#x20;

Processing Link: [https://processing.org/reference/noise\_.html](https://processing.org/reference/noise\_.html)

> Perlin noise has a more organic appearance because it produces a naturally ordered (“smooth”) sequence of pseudo-random numbers. The graph below shows Perlin noise over time, with the x-axis representing time; note the smoothness of the curve. \
> [Khan Academy](https://www.khanacademy.org/computing/computer-programming/programming-natural-simulations/programming-noise/a/perlin-noise)

Images below from Khan Academy - Show how noise ( ) differs from random( )

[https://www.khanacademy.org/computing/computer-programming/programming-natural-simulations/programming-noise/a/perlin-noise](https://www.khanacademy.org/computing/computer-programming/programming-natural-simulations/programming-noise/a/perlin-noise)

![](https://cdn.kastatic.org/ka-perseus-images/0fd97fc7ab7ac5a7670935f1695d2a0c614e5252.png)

![](https://cdn.kastatic.org/ka-perseus-images/81e9d201147cd09f1b78f9541993d8460355eb3e.png)



```
void updateArray_Display(  ){
  int maxFC1 = 100;
  int maxFC2 = 50;
  float noiseFC1 = noise(frameCount)*5;
  
  //uncomment to see how noise values change
  //println("FC " + frameCount + " NoiseFC1+frameCount%time2 " + (noiseFC1+frameCount)%maxFC1 + " noiseFC1 " + noiseFC1); 
  
  //use the changing noise signal in the map function
  float fractionFC = map((noiseFC1+frameCount)%maxFC1, 0, maxFC1-1,0.0,1.0);
  float fractionSize = map(noiseFC1+(frameCount%maxFC2),0, (maxFC2-1)/2,0.3,1.0);
  
  float mXHue = map( mouseX, 0,width, 80,185);
  accentMx = color(mXHue,90,70,50); 
  color curColor1=lerpColor( purple, aqua, fractionFC);
  color curColor2 =lerpColor( aqua, accentMx, fractionSize);
  int rows = 8;
  int cols = 8;
  float cellSize = width/cols;
  
  PShape[][] myShapes1 = new PShape[rows][cols]; //num elements is rows*cols
  PShape[][] myShapes2 = new PShape[rows][cols]; //num elements is rows*cols
 
  populate2DArray1( myShapes1, rows, cols, cellSize*fractionSize, curColor2, curColor1);
  populate2DArray2( myShapes2, rows, cols, cellSize*fractionSize, curColor2, curColor1);
 
  pushMatrix();
  scale( 0.5,0.5);
  displayShapeMatrix( myShapes1, rows, cols, cellSize);
  popMatrix();
  
  
  pushMatrix();
  translate(width, 0); //move origin to upper right
  scale( -0.5,0.5);
  displayShapeMatrix( myShapes2, rows, cols, cellSize);
  popMatrix();
  
  
  pushMatrix();
  translate(0, height); //move origin to upper right
  scale( 0.5,-0.5);
  displayShapeMatrix( myShapes2, rows, cols, cellSize);
  popMatrix();
  
  pushMatrix();
  translate(width, height); //move origin to upper right
  scale( -0.5,-0.5);
  displayShapeMatrix( myShapes1, rows, cols, cellSize);
  popMatrix();
}

```
