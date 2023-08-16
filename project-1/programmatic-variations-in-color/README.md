# Project 1: Programmatic Variations in Color

Using HSB ColorMode allows us to configure and modify colors in our programs based changing values for the Hue, Saturation, or Brightness.

## Gradients:

If we use a gradient (programatic change) for the brightness of an abstract pattern, we can enhance the illusion of depth for 2D designs.

Since we're using `float len` as an input parameter to determine the size of the shape, we can also use this value of len to help determine a good value to control varying the brightness each time we drawn a shape. One way to do this is to set the max value for Brightness using the max value for Len:

## Map Function

In the example below, we are creating a relationship between the current value of len, the maximum len value: lenMax, and the max value for brightness to determine the brightness value for a current value of len. This is exactly what the Map function does, it creates a linear mapping between 2 ranges of values. So, as long as we have access to the range of each set of values, we can use the processing map function to programmatically determine color for our vertexPatterns. To control the hue, we're using the map function to create a relationship between the mouseX position and we're constraining the hue to a narrow range between blue and pink (Hue between 200,300);

## LerpColor Function

Processing provides a function LerpColor( ) to create gradients of color between 2 color endpoints. Lerp means Linear interpolation: which means each intermediate color

![](<../../.gitbook/assets/Screen Shot 2018-09-04 at 12.17.58 PM.png>)

```java
float lenMax, lenMin;
color c1;

void setup(){
    size( 600, 600);
    colorMode( HSB, 360, 100, 100 ); 
    c1 = color( 270, 100, 100);
    lenMax = 150;
    lenMin = 20; 
}

void draw(){
    //draw nested vertexShapes at mouse position
    if(mousePressed){
      translate(mouseX, mouseY);
      //can add region: color, size logic here

      recursivePattern(lenMax,5, c1);

      resetMatrix();
      }
}

void recursivePattern( float len, int count, color c1){
  if( count< 1){
    return;
  }
  //set fill before calling vertexShape function
  float fraction = map( len, lenMin, lenMax, .2, 1.0);

  color curColor = color(hue(c1), saturation(c1), brightness(c1)* fraction);

  PShape s= vertexShape( len, curColor); //task - draw shape
  //can add rotation, scale logic here

  shape( s, 0,0);  //this displays the shape on the canvas at point (0,0)

  recursivePattern( len*.8, count-1, c1); //Recursive call
}

PShape vertexShape( float len, color c1){
   fill(c1);
   PShape s = createShape(RECT, 10, 10, 100, 100); //placeholder shape
   return s; 
}
```
