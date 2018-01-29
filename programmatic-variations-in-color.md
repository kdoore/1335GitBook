#Programmatic Variations in Color

Using HSB ColorMode allows us to configure and modify colors in our programs based changing values for the Hue, Saturation, or Brightness.

For Project 1, We're using recursion to create a series of PShape objects, where we modify the shape's length parameter with each recursive call.   The code below shows that when we set the colorMode to HSB, we also have the ability to set the maximum value for each of the parameters, and this is one way we can control color for our patterns:  colorMode( HSB, HueMax, SatMax, BrightMax).  One choice for setting these values is to use ColorMode(HSB, 360, 100,100) because this corresponds to the HSB values in the processing color selector tool.


```java

void setup(){
    size( 600,600);
    float lenMax = 200;
    colorMode( HSB, HueMax, SatMax, BrightMax); //What are these values: ?
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
    s.vertex( len/4,0);
    s.vertex( len/2, len/2);
    s.vertex( 0, len/4);
    s.endShape( CLOSE);
    shape( s, 0, 0);
}

```

###Map Function
In the above example, we are essentially creating a relationship between the current value of len, the max len value: lenMax, and the max value for brightness to determine the brightness value for a current value of len.  This is exactly what the Map function does, it creates a linear mapping between 2 ranges of values.  So, as long as we have access to the range of each set of values, we can use the processing map function to programmatically determine color for our vertexPatterns.  

```java
//define global variables for use in map( )

float lenMax;
float hueMin, hueMax;
float brightMin, brightMax;

void setup(){
    lenMax = 200;
    lenMin = 30;
    hueMin = 100; //green
    hueMax = 160; //cyan
    brightMin = 50;
    brightMax = 100;

    colorMode( HSB, 360, 100, 100 ); //use ColorSelector HSB ranges
    vertexPattern( lenMax);
    vertexPattern( lenMax - 50);
}
void vertexPattern( float len){
//use map function to determine how hueVal, brightVal vary with changes in len.  
    float hueVal = map( len, lenMin, lenMax, hueMin, hueMax);
    float brightVal = map( len, lenMin, lenMax, brightMin, brightMax); 
    PShape s = createShape();
    s.beginShape();
    s.fill(hueVal, 100 , brightVal );// fully saturated custom color, with brightness dependent on the len input parameter.
    s.vertex( 0,0);
    s.vertex( len/4,0);
    s.vertex( len/2, len/2);
    s.vertex( 0, len/4);
    s.endShape( CLOSE);
    shape( s, 0, 0);
}

```






