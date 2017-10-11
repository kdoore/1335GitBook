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

###map( ) Function
The Processing `map( )` function can be helpful in calculating the lerpColor fractional amount parameter since the value must be between the range `[0.0, 1.0]`  Often we'll have a different range of values that we'd like to use to control how the color varies.  If we're creating a diagonal gradient for a grid, we may want to use a variable that represents the sum of loop index terms:  `int k = i + j;`   The values of i, j, and k depend on the number of rows and columns that we're working with.
 
###Use map( ) to determine lerpColor fractional value
The code below shows how we can use the map function to determine a valid value for fractional amount for intermediate color. 

map takes one value in a given range and calculates the corresponding value for a second range.  In this case, we have the value of k, we know it can range from 0 to rows+cols. When i, j are at their max values, then `k = rows + cols - 2`. We need to subtract 2 because i and j are indexes and the numbering ranges from 0 to rows.length-1, or O to cols.length-1  We know that range2 is the value we're trying to find, it corresponds to the range (0.0 to 1.0).  Map calculates this for us when used as below. 
 
 `float value2 = map( value1, range1Min, range1Max, range2Min, range2Max); `
 
 `float amt = map( k, 0, rows+cols, 0.0, 1.0);`
 
###Example Code 
```
 color startColor = color(180, 100,100); //bright cyan
  color endColor = color(75, 90, 70); //pea green
  for( int i = 0; i < rows; i++){
    for( int j = 0; j < cols; j++){
      int k = i + j;
      float amt = map( k,0,rows + cols-2, 0.0, 1.0);
      color intermediateColor = lerpColor( startColor, endColor, amt);
      fill(intermediateColor);
      rect( i* size, j * size, size, size);
    }
  }
  
```
###Grid Gradient using lerpColor( ) and map( )
The image below shows i,j values and the corresponding lerpColor fractional amount that was calculated using the map function in the code above.

![](/assets/Screenshot 2017-09-24 17.00.20.png)
  
  


