#Programmatic Variations in Color

Using HSB ColorMode allows us to configure and modify colors in our programs based changing values for the Hue, Saturation, or Brightness.

###Gradients:  Brightness Max = LenMax.
If we use a gradient for the brightness of an abstract pattern, we can enhance the illusion of depth for 2D designs.  

Since we're using `float len` as an input parameter to determine the size of the shape, we can also use this value of len to help determine a good value to control varying the brightness each time we drawn a shape.  One way to do this is to set the max value for Brightness using the max value for Len:

###Map Function
In the example below, we are creating a relationship between the current value of len, the maximum len value: lenMax, and the max value for brightness to determine the brightness value for a current value of len.  This is exactly what the Map function does, it creates a linear mapping between 2 ranges of values.  So, as long as we have access to the range of each set of values, we can use the processing map function to programmatically determine color for our vertexPatterns.  To control the hue, we're using the map function to create a relationship between the mouseX position and we're constraining the hue to a narrow range between blue and pink (Hue between 200,300);


![](/assets/Screen Shot 2018-09-04 at 12.17.58 PM.png)

```java

float lenMax;
void setup(){
    lenMax = 150;
    colorMode( HSB, 360, 100, 100 );  
}

void draw(){
    //draw nested vertexShapes at mouse position
      translate(mouseX, mouseY);
      recursivePattern(lenMax,5);
      resetMatrix();
}

void recursivePattern( float len, int count){
  if( count< 1){
    return;
  }
  //set fill before calling vertexShape function
  float bright = map( len, 0, lenMax, 0, 100);
  float hue = map( mouseX, 0, width, 200, 300);
  fill(hue, 100, bright);// brightness dependent on the len input parameter.

  vertexShape( len); //task - draw shape
  recursivePattern( len*.8, count-1); //Recursive call
}


void vertexShape( float len){
   PShape s = createShape(RECT, 10, 10, 100, 100); //placeholder pattern
    shape( s, 0,0);  //this displays the shape on the canvas at point (0,0)
}

```







