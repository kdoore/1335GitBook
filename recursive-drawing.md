###Recursive Patterns:
With Recursion, we can often think of a set of rules being executed for each function call. This can be used to create interesting patterns, because we can often decompose graphic patterns to be expressed as a set of rules.  In the artwork below, a simple pattern of concentric rectangles is created wherever the mouse is pressed. 

![](Screenshot 2016-01-23 09.23.52.png)

###Recursive Pattern Drawing Application 

The recursive function: `Pattern(length, level)` takes input parameters that control the size of the rectangle and an integer value `level`, which controls the number of concentric rectangles drawn.  By adding slight random variation in the rotation angle, rectangle size, and hueValue of the fill and stroke for each drawn rectangle, the user can create a unique artwork each time they run the program.  The hueValue can be mapped to the `x` position of the mouse.  Using the `Hue, Saturation, Brightness: colorMode(HSB)` allows for slight random variations of the hueValue to give slight variations in the hue of the drawn pattern.  

### Main Program Structure

1. When the user presses the mouse

```java
void Draw(){  //use processing Draw function
    if ( mousePressed){
    //draw a pattern 
    }
}
```

2. Move the canvas origin to the current mouse position. 
  
    ```java
    translate(mouseX, mouseY);
     ```

3. Draw some pattern based on ``length`` parameter, by **calling** the recursive function: recursivePattern( );
    
```java 
        
    recursivePattern( 100, 5); //Recursive Pattern Called 
```
       
4. Move Origin back to upper left corner
     ```java
    resetMatrix();
    ```

### Define Recursive Function
Here we **define** a recursive function: `recursivePattern` so that it calls itself for `level` number of times, with a `length` parameter that determines the pattern size:

    ```java
        
    void recursivePattern( float length, int level) {
    
    ```
        
1. We need to add a **test for the termination condition **as the first task in the function:     
        
    ```java
    if(level <= 0) { 
        return; //stops recursion
    }
     ```
2.  We will **draw a shape at the origin using the ``length`` parameter**  
        
    ```java
    fill( 255, 255, 100);// set some fill color
    rect( 0, 0, length, length); //draw at origin, use length parameter
    ```
        
3. Call recursive function, within the function itself, make sure to modify the function parameters:             

    - **change length:** length * 0.8  
    - **change level:**  level - 1 
    
      ```java
       recursivePattern( length * 0.8, level - 1 );   
       ``` 
                
                
### Complete Program

```java

void setup(){
  size( 600,600);
  colorMode(HSB); 
  }
  
  void draw(){
    if(mousePressed){
      translate(mouseX, mouseY); 
          recursivePattern( 100, 5);   //call recursive function
      resetMatrix();
    }
  }
  
  //define recursive function
  void recursivePattern( float length, int level){
    if ( level <= 0 ){  //test for termination
      return; //termination condition is true
    }
    fill( (mouseX + length) % 255 , 255, 255, 100);  
    rect( 0, 0, length, length);  //draw a pattern based on length parameter
    recursivePattern( length * 0.8, level -1); //call recursive function
    }
    
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
