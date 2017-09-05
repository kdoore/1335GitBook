###Recursive Patterns:
With Recursion, we can often think of a set of rules being executed for each function call. This can be used to create interesting patterns, because we can often decompose graphic patterns to be expressed as a set of rules.  In the artwork below, a simple pattern of concentric rectangles is created wherever the mouse is pressed. 

![](Screenshot 2016-01-23 09.23.52.png)

###Recursive Pattern Drawing Application 

The recursive function: `Pattern(length, level)` takes input parameters that control the size of the rectangle and an integer value `level`, which controls the number of concentric rectangles drawn.  By adding slight random variation in the rotation angle, rectangle size, and hueValue of the fill and stroke for each drawn rectangle, the user can create a unique artwork each time they run the program.  The hueValue is mapped to the `x` position of the mouse.  Using the `Hue, Saturation, Brightness: colorMode(HSB)` allows for slight random variations of the hueValue to give slight variations in the hue of the drawn pattern.  

Simplified rules for the pattern drawn above are:

1. When the user presses the mouse

    ```java
    if ( mousePressed){
        //draw a pattern 
    }
    ```

2. Move the canvas origin to the current mouse position. 
  
        ```java
        translate(mouseX, mouseY);
         ```

3. Draw a Pattern based on ``length`` parameter, at the origin ( we just moved the origin to the mouse position)
    
    ```java
        rect(0,0,length, length);
    ```
        
4. Then we need to add a recursive call to Pattern so that it calls itself for `level-1` number of times, with a smaller value of length:
        - Pattern( length * .8, level-1) 
5. We need to add a test for the termination condition as the first task in the function:     
        ```java
        if(level <= 1) { return }
        ```
       
6. Move Origin back to upper left corner
         ```java
        resetMatrix();
        ```

###Save Drawing
If we want to save our image, we can use the processing save() function and we can call it whenever we press a certain key, like 's'.  This will save our image to our sketch folder. The file can be saved in a variety of file formats.
[Processing Reference: save()](https://processing.org/reference/save_.html)

```java
void keyPressed(){
  if( key == 's' || key == 'S'){
    save("big.png");
  }
  
  ```
