#lerpColor( ) and map( ) Functions

Processing provides a function that creates a series of intermediate colors between 2 colors at a specific increment.  The lerpColor( ) function calculates a linear interpolation between 2 color values.  This will make our task for creating gradient patterns much easier.  

###Problem - how to create gradient based patterns 
Our first attempt used a hue variable that we incremented within a for-loop, where the fill for our pattern was defined using colorMode(HSB);

![](/assets/Screenshot 2017-09-24 15.33.05.png)
![](/assets/Screenshot 2017-09-24 15.36.26.png)

Hue >= 255  corresponds to Red
Hue <= 0    correspond to Red
    
Problems occurred when we reached hue values greater than 255, as all shapes were then colored red.  We could create our own work-arounds, such as using modulus to insure hue values stayed in 0-255 range.  Other problems occurred if we wanted to have colors that varied in all HSB parameters.     

```java
//Code Snippets - Initial Attempt - Increment Hue
  int hue = 50;
    for( int i=0; i< numShapes; i++ ){
       shapes[i] = vertexPattern( size, hue);
       hue += 5;
   }
  
  PShape vertexPattern( float len, int hue){
      fill( hue, 255 , 255);
      //more code
  }
```

###Using lerpColor( color c1, color c2, float amount) 
lerpColor takes 2 color values as input parameters, and takes a floating point fractional value to indicate the fractional distance between the 2 colors to calculate the intermediate color that is returned.

![](/assets/Screenshot 2017-09-24 16.01.04.png)

Using the colorSelector tool, we need to make sure to set HSB as below. This sets the range of values for Hue: 0-260, Sat: 0-100, Brightness: 0-100

`colorMode(HSB, 360, 100, 100 ); //corresponds to the colorSelector color values`

Logic for image above:  

1. Select a start and end colors
     
  `color startColor = color(180, 100,100); //bright cyan`
  `color endColor = color(75, 90, 70); //pea green`
  
2. Set (and modify) the amount variable - it takes decimal values between 0.0 - 1.0
 
 `float amt = (.10 * i );  //i is loop index `
 
3.  Determine calculated color:
  
  `color interColor = lerpColor( startColor, endColor, amt);`
  
4.  The first square shows the startColor since `amt = 0.0`

5.  The last square shows the endColor since `amt = 1.0`
  
###Example Code

```java
for( int i=0; i<= 10; i++){
      float amt = i * 0.1;
      color intermediateColor = lerpColor( startColor, endColor, amt);
      fill(intermediateColor);
      rect( i* size, 0, size, size);
      }
```


  
  
  


