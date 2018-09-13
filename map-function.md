#Map Function - Create relationships between variables

The Processing map function is a very useful function which converts a value from one range into a corresponding value in a second range. [processing.org: map function](https://processing.org/reference/map_.html) 

###Map Function - Parameters
The map function takes 5 input parameters:  the first 3 values correspond to the known value in first range, and the first range endpoints.  The last 2 values are the 2 endpoints for the second range.  

```java

float Map( float value, float start1, float end1, float start2, float end2) 
```
In the image below, we can see a visual illustration of the map function with parameter values listed below: 

float value2 = map( value1, 50, 200, 10, 360);

![](/assets/Screen Shot 2018-09-13 at 1.18.40 PM.png)

We can see that if value1 = 157, then value2 is calculated to be 259.

We can use the Map function to create relationships between features of our programs.  

In Project 1, we can use the changing value of the length parameter for drawn patterns as the known value that is changing, we can use it to give us changing values of color components, such as hue, saturation, or brightness. 

```java
  
  float hue = map(mouseX, 0,width, 100, 250);
  float bright = map(len, 5, lenMax, 100,50);
  float sat = map(len, 5, lenMax, 100,20);
 
  fill( hue, sat, bright );
```


###Example code for MapExample
Below is the code used in the Map Example image above

```java

 int r1y  = 50;
int r2y  = 80;
int r1Start = 50;
int r1End = 200;
int value1;
int r2Start = 10;
int r2End = 360;
int value2;

void setup(){
  size( 400,200);
  colorMode(HSB, 360,100,100);
  strokeWeight(2);
  
}

void draw(){
  background(255);
  fill(0);
  stroke(0);
  //range1 and endpoints
  line( r1Start, r1y, r1End, r1y);
  ellipse( r1Start, r1y, 5, 5);
  ellipse( r1End, r1y, 5,5);
   
   //range2 and endpoints
  line( r2Start, r2y, r2End, r2y);
  ellipse( r2Start, r2y, 5, 5);
  ellipse( r2End, r2y, 5,5);

  stroke( 150);
  line( value1, r1y, value2,r2y); //line connecting values
  fill(0,100,100);
  value1 = constrain(mouseX, r1Start, r1End); //restrict value1 to range1
  ellipse( value1, r1y, 10,10); //ellipse to mark value1
  value2 =(int) map( value1, r1Start, r1End, r2Start, r2End);
  ellipse( value2, r2y, 10, 10); //ellipse to mark value2
  
  ///text to display values
  fill(0);
  text( r1Start, r1Start-10, r1y-5);
  text( r1End, r1End-10, r1y-5);
  text( r2Start, r2Start-10, r2y-5);
  text( r2End, r2End-10, r2y-5);
  text( "value1 " + (int)value1, 10, 20);
  text( "value2 " + (int)value2, 10, 120); 
  
} 

```







