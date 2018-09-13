#Map Function

The Processing map function is a very useful function which converts a value from one range into a corresponding value in a second range. [processing.org: map function](https://processing.org/reference/map_.html) 

###Map Function Signature
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


 






