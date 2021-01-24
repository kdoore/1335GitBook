# HSB Color Mode

### Processing Color Modes

Processing provides functions to allow working with both ****[**RGB and HSB color-spaces**](https://processing.org/reference/colorMode_.html)**. HSB color-space** is very useful when trying to create visual designs through programming. We will use it extensively in this course.  HSB has color components: Hue, Saturation, Brightness. The HSB parameters are useful for mapping to encode relationships between concepts, interactions.  HSB simplifies the cognitive load because it aligns with familiar color concepts such as roygbiv ordering of natural light in a rainbow.

![](../../.gitbook/assets/hsb_cone.png)

Image from: [TomJewett.com](http://www.tomjewett.com/colors/hsb.html)

### HSB Color

The image above shows the HSB color-space. From this diagram, we can see that if we want to understand a specific HSB color, in terms of Hue, Saturation, and Brightness parameter values, it is easiest to read a HSB color starting with the brightness parameter which corresponds to the vertical axis of the color-cone.

**Example Code using HSB colorMode and color compliment logic** 

```java
float hue;
void setup(){
  size(600,600);
  colorMode(HSB, 360,100,100);
  rectMode(CENTER); //draw rect from center
}

void draw(){
  hue = mouseX  % 360; //insure hue < 360, dependent on mouseX
  background( hue, 100, 100); //background
  fill((hue + 180)%360, 100, 100); //complimentary color
  translate( width/2, height/2);
  rect(0 ,0, mouseY, mouseY); //size dependent on mouseY position
}
```

## Analyze HSB Color in Brightness, Saturation, Hue Order

When trying to interpret the value associated with an HSB color value, we should start with the Brightness value, If it's non-zero, then we should proceed to analyze the Saturation value, if it's non-zero, then we should consider the Hue value. If Brightness is 0, then the corresponding HSB color is black. If B is non-zero, then the color is located higher in the color cone, so we can visualize moving up the cone along the vertical axis, by a value corresponding to the B value. The Saturation value controls movement outward along the radius of the cone. If Saturation is 0, then we're at the center-axis and all colors have no saturation, they are grayscale colors. If Saturation is non-zero, then we need to analyze the Hue value to understand the hue color value. When Hue = 0, or Hue &gt;= 255, the color is Red. Otherwise, the color follows the Rainbow pattern: ROYGBIV -

## Processing ColorMode\(HSB\)

To use HSB in processing, we need to set the colorMode property to HSB mode: `colorMode(HSB)`. In addition, processing provides a method for us to set the max range values for HSB colormode, by default, each value can range from 0-255, just as with RGB. Since the processing color selector tool uses HSB with ranges: Hue: 0-360, Sat: 0-100, Bright: 0-100, if you'll be using the colorSelector to choose color values, you can set these range max values when you specify colorMode: `colorMode(HSB, 360, 100, 100);` //sets range max so they correspond to the colorSelector tool.

## Brightness

The brightness scale defines grayscale colors, where a brightness value of 0 corresponds to black, and the max-brightness corresponds to white. So, if we see an HSB value with 0 for brightness, the other values \(H,S\) don't have an impact on the color because the colorspace is at the lowest tip of the cone, and black is the only color in this region. So for a fill\(\) function with 3 values fill\(H, S, B\), we should start reading the color from the right-most parameter, the B value. If the B value is 255 \(the max value\), then we can see that these colors correspond to the top surface of the cone.

## Saturation

Within this circular slice, we can see that the center of the circle is white, and as the radius increases, the saturation increases so the outer rim of the circle has full saturation values. So, when analyzing an HSB value, once we've determined that B is greater than 0, we next need to look at the S value to determine the saturation level. This corresponds to moving outwards from the center-point of the circle, to colors with higher saturation intensity.

## Hue

The Hue value corresponds to the angle of rotation around the circle. This image shows the hue angle with the opposite orientation than what is used for the Processing language. In Processing, the hue values increase in the clockwise direction, with the 0 value at the 3 o'clock position, and this corresponds to the color red. The default range for HSB input parameters is 0-255. So, when looking at the angular position of a a color, we need to remember to scale the colors so that the 0-360 color range is mapped to the variable range: 0-255. We can either write a math equation for this conversion or we can use the Processing [map\(\)](https://processing.org/reference/map_.html) function.

```text
colorMode(HSB);
var hueAngle=30;
var hueValue =( (hueAngle) / 360) * 255;
```

## Map\( \)

We can use the map\( \) function to convert a value from it's current range to a target range. If we start with an input hueAngle, and we want to convert it to an 8 bit, 0-255 target range, then we write the function as shown below. See additional examples using [map\( \)](https://processing.org/examples/map.html) on the processing.org

```text
    // map(inputValue, valueStart, valueStop, targetStart, targetStop)
    hueValue= map(hueAngle, 0, 360, 0, 255);
```

In a similar manner, we can use map\( \) to determine the hue value based on the x position of the mouse:

```text
   hueValue=map(mouseX, 0, width, 0, 255);
```

