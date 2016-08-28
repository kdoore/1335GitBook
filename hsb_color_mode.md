#HSB Color Mode
![](HSB_Cone.png)

Image from: [TomJewett.com](http://www.tomjewett.com/colors/hsb.html)

Processing provides functions to allow working with both [RGB and HSB color-spaces](https://processing.org/reference/colorMode_.html).  HSB color-space is very useful when trying to create visual designs through programming.  

###HSB Color 
The image above shows the HSB color-space.  From this diagram, we can see that if we want to understand a specific HSB color, in terms of Hue, Saturation, and Brightness parameter values, it is easiest to read a HSB color starting with the brightness parameter which corresponds to the verticle axis of the color-cone.  

###Brightness
The brightness scale defines grayscale colors, where a brightness value of 0 corresponds to black, and the max-brightness corresponds to white.  So, if we see an HSB value with O for brightness, the other values (H,S) don't have an impact on the color because the colorspace is at the lowest tip of the cone, and black is the only color in this region.  So for a fill() function with 3 values fill(H, S, B), we should start reading the color from the right-most parameter, the B value.  If the B value is 255 (the max value), then we can see that these colors correspond to the top surface of the cone.  

###Saturation
Within this circular slice, we can see that the center of the circle is white, and as the radius increases, the saturation increases so the outer rim of the circle has full saturation values.  So, when analyzing an HSB value, once we've determined that B is greater than 0, we next need to look at the S value to determine the saturation level.  This corresponds to moving outwards from the center-point of the circle, to colors with higher saturation intensity.  

###Hue
The Hue value corresponds to the angle of rotation around the circle.  This image shows the hue angle with the opposite orientation than what is used for the Processing language.  In Processing, the hue values increase in the clockwise direction, with the 0 value at the 3 o'clock position, and this corresponds to the color red.  The default range for HSB input parameters is 0-255.  So, when looking at the angular position of a  a color, we need to remember to scale the colors so that the 0-360 color range is mapped to the variable range: 0-255.  We can either write a math equation for this conversion or we can use the Processing [map()](https://processing.org/reference/map_.html) function.

``` 
colorMode(HSB);
var hueAngle=30;
var hueValue =( (hueAngle) / 360) * 255;
```
###Map( )
We can use the map( ) function to convert a value from it's current range to a target range. If we start with an input hueAngle, and we want to convert it to 
an 8 bit, 0-255 target range, then we write the function as shown below.  See additional examples using [map( )](https://processing.org/examples/map.html) on the processing.org 

```
    // map(inputValue, valueStart, valueStop, targetStart, targetStop)
    hueValue= map(hueAngle, 0, 360, 0, 255);
```
In a similar manner, we can use map( ) to determine the hue value based on the x position of the mouse:
```
   hueValue=map(mouseX, 0, width, 0, 255);
   ```
