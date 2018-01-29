#Programmatic Variations in Color

Using HSB ColorMode allows us to configure and modify colors in our programs based changing values for the Hue, Saturation, or Brightness.

For Project 1, We're using recursion to create a series of PShape objects, where we modify the shape's length parameter with each recursive call.   


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



