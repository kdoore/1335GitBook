#Modulus
[Processing Documention](https://processing.org/reference/modulo.html)
We'll use the integer version of Modulus in this course.  In this case, modulo is an operator that calculates the remainder, for integer division ( long division ).  Integer division calculates how many times the top number (numerator ) can be divided by the bottom number (divisor ).  The modulus is the remaining value, and it is very useful in Computer Science.

Modulus Example:  

```java
int remainder = 7 % 4;
println( remainder ); //  remainder is 3
```



It's helpful to list out the modulus for a variety of values:  

   0 % 4 == 0
   1 % 4 == 1
   2 % 4 == 2
   3 % 4 == 3
   4 % 4 == 0
   5 % 4 == 1
   123 % 4 == 3
   
  We can observe that anyNumber % 4 will have values that range between 0, 3.   This is convenient because it is a 0 based range of values, which can be used to calculate array index values.
  
     anyNumber % arrayLength == valid array index   


###Modulus Code Example - Array indexes: 
The code below uses modulus to set values for the **variable: index** used in the draw function.  index is calculated using frameCount, which is an increasing integer that tracks the number of frames that have been rendered since the program started.  Modulus is helpful for arrays since it calculates a variable 


```java
color[] colors;

void setup(){
  size( 400, 400);
  colorMode(HSB, 360, 100, 100);
  colors = new color[3];//initilize:  how many elements
  colors[0] = color( 100, 100, 100);
  colors[1] = color( 200, 100, 100);
  colors[2] = color( 300, 100, 100);
  }
  
 void draw(){
   frameRate(2);
   int index = frameCount % 3;
   color tempColor = colors[index];
   fill(tempColor);
   rect( 0,0,width, height);
   println(frameCount);
 }
```

