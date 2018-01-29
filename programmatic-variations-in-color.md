#Programmatic Variations in Color

Using HSB ColorMode allows us to configure and modify colors in our programs based changing values for the Hue, Saturation, or Brightness.

For Project 1, We're using recursion to create a series of PShape objects, where we modify the shape's length parameter with each recursive call.   The code below shows that when we set the colorMode to HSB, we also have the ability to set the maximum value for each of the parameters, and this is one way we can control color for our patterns:  colorMode( HSB, HueMax, SatMax, BrightMax).


```java

void setup(){
    size( 600,600);
    float lenMax = 200;
    colorMode( HSB, HueMax, SatMax, BrightMax); 
    VertexPattern( lenMax );
    VertexPattern( lenMax - 50);
}

void vertexPattern( float len){
    PShape s = createShape();
    s.beginShape();
    s.fill( ?, ?, ? );//what values for HSB can be set here to change shape's color in a meaningful way?
    s.vertex( 0,0);
    s.vertex( len/2, len/2);
    s.vertex( len/4, 0);
    s.endShape( CLOSE);
    shape( s, 0, 0);
}

```


###Brightness Gradient:  BrightnessMax = LenMax.
If we use a gradient for the brightness of an abstract pattern, we can enhance the illusion of depth for 2D designs.  

Since we're using `float len` as an input parameter to determine the size of the shape, we can also use this value of len to help determine a good value to control varying the brightness each time we drawn a shape.  One way to do this is to set the max value for Brightness using the max value for Len:

```java

float lenMax;
void setup(){
lenMax = 200;
colorMode( HSB, 360, 100, lenMax );  //use max value: lenMax to set max value for Brightness in setup
vertexPattern( lenMax);
vertexPattern( lenMax - 50);
}
void vertexPattern( float len){
    PShape s = createShape();
    s.beginShape();
    s.fill(0, 100, len );// fully saturated red color, with brightness dependent on the len input parameter.
    s.vertex( 0,0);
    s.vertex( len/2, len/2);
    s.vertex( len/4, 0);
    s.endShape( CLOSE);
    shape( s, 0, 0);
}

```










