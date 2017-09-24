#lerpColor( ) and map( ) Functions

Processing provides a function that creates a series of intermediate colors between 2 colors at a specific increment.  The lerpColor( ) function calculates a linear interpolation between 2 color values.  This will make our task for creating gradient patterns much easier.  

###Problem - how to create gradient based patterns 
Our first attempt used a hue variable that we incremented within a for-loop, where the fill for our pattern was defined using colorMode(HSB);

![](/assets/Screenshot 2017-09-24 15.33.05.png)
![](/assets/Screenshot 2017-09-24 15.36.26.png)

Hue >= 255  corresponds to Red
Hue <= 0    correspond to Red
    
Problems occurred when we reached hue values greater than 255, as all shapes were then colored red.  We could create our own work-arounds, such as using modulus to insure hue values stayed in 0-255 range.  Other problems occurred if we wanted to have colors that varied in all HSB parameters.     

```
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

If we set colors using the colorSelector tool, we need to make sure to set HSB as below.

`colorMode(HSB, 360,100,100); //corresponds to the colorSelector color values`

