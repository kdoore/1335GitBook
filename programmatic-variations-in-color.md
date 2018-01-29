#Programmatic Variations in Color

Using HSB ColorMode allows us to configure and modify colors in our programs based changing values for the Hue, Saturation, or Brightness.

For Project 1, We're using recursion to create a series of PShape objects, where we modify the shape's length parameter with each recursive call.   The code below shows that when we set the colorMode to HSB, we also have the ability to set the maximum value for each of the parameters, and this is one way we can control color for our patterns:  colorMode( HSB, HueMax, SatMax, BrightMax).


```java
 

void setup(){
    size( 600,600);
    float len = 200;
    colorMode( HSB, HueMax, SatMax, BrightMax); 
    VertexPattern( len );
    VertexPattern( len - 50);
}

void VertexPattern( float len){
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
###Brightness Gradient to enhance depth in design.
If we use a gradient for the brightness of an abstract pattern, we can enhance the illusion of depth for 2D design.  Since we're using `float len` as an input parameter to determine the size of the shape each time it's drawn, we can also use this value of len to help determine a good value varying the brightness at each time we drawn a shape.  






