#2D Arrays for Gradient Grid Patterns

After creating our mini-pattern preview, it might inspire us to rethink the complex logic that we've been using for creating regions in our designs. This will begin our transition into object oriented thinking.

###New Idea: Position ShapeGrids with Transform Functions 

Instead of having complex logic within a single display-function's for-loop, let's create a set of simplified grid modules and position them using Processing's transform functions.  This can lead us to simplified logic, which can allow for more complex patterns.  In addition, we can implement logic for layering patterns on top of other patterns to achieve complex designs from simplified logic.  

###Grid Sections - Translated, Rotated, Scaled
In the image below, one grid pattern is used multiple times to create the entire design pattern. The basic grid section is displayed normally in region1.  The same grid section is also used in region2, region3 and region4...where rotations, translations, and offsets change the orientation and position.  Finally, 4 additional grid sections are used to create the inner design, this section is scaled to quarter size, it's rotated by 45 degrees, and it's translated to the center of the design.

![](/assets/Screenshot 2017-09-24 14.58.17.png)

###1-Dimensional Arrays - Design Limitations
As seen in the image below, when we have a linear ordering for our colors (1-Dimensional array), then when we display those in a grid we see this linear ordering, which we perceive as rows of (grayscale) colors. This is a linearity is a limitation if we want more complex color relationships between neighboring cell items.


![](/assets/Screenshot 2017-09-24 13.42.33.png)


###2-Dimensional Arrays for Storing our Shapes
Now is a good time to consider switching to 2-Dimensional arrays to store our modular design units. 
If we create our and store our shapes using a 2-Dimensional data-structure , then we can store higher-order relationships between our design units, such as 2-D color gradients. 

Example:  Declare and initialize a 2D array of 100 elements, to hold PShape objects.

`PShape[][] shapesMatrix = new PShape[10][10];`

###Diagonal Color Gradients
![](/assets/Screenshot 2017-09-24 08.43.41.png) 

###Define variable k to determine color pattern.
In the image above, we see a diagonal color gradient in both the foreground and background colors. The logic associated with this can be seen in the image below.  If we define a new variable: `int k = i + j;` , where k is the sum of the i, j index variables, we see that the value of k increases along the grid's diagonal direction.  Then we can **use k as a factor to determine the fill color**. 

###Color Gradient Logic:
Using the sum of grid indexes for color logic gives us a simple approach to create complex patterns.  We can observe a pattern that forms when we consider i,j indexes of each cell:  if we add i + j indexes for a cell, then neighboring cells along diagonal lines have equal values of i + j.  We can use this relationship to determine fill values for cells, so we can create a gradient fill diagonally across a grid of cells.  
    

```java
      int k= i + j; //i,j are for-loop indexes
      fill( 150 + (k * 10) );  //gradient logic
```

![](/assets/Screenshot 2017-09-24 09.00.41.png)

###Odd-Even Gradient Logic
We can also use this sum variable: `k` for determining odd-even logic.  When we use the modulus operator `%`, we focus on the remainder component, so when `k%2` has no remainder `( k%2 == 0 )`, we have a way to implement odd-even logic in our patterns. In the image below, we've combined it with the gradient color fill logic. If we  have an _odd_ item, then we use a light gray `fill(240)`, otherwise, we use our gradient logic to create our fill.

```java
      int k= i + j;  //i,j are for-loop indexes
      if(k % 2 == 0){
         fill( 100 + k *10); //gradient logic
      }
      else{
         fill(240); //light gray
      }
```


![](/assets/Screenshot 2017-09-24 09.08.55.png)


###Random Patterning Logic 
In the images below, we can see that there are 2 different design units, shape1 has 2 colored vertically-stacked triangles on a dark background, shape 2 is a rotation - so the colored triangles have left/right orientation.  
By randomly selecting between these units, we have an additional design pattern. 

![](/assets/Screenshot 2017-09-24 14.01.11.png)  
Shape1  ... Shape2

![](/assets/Screenshot 2017-09-24 14.02.04.png)

###Logic for Randomized 2-pattern arrangement:
We can use the Processing random(min,max ) function to simulate random events. We define and initialize a random variable: `rand` that will be assigned a decimal value between 0.0 and 2.0.   We determine that if `rand > 1`, then we `vertexPattern1( )`, like a coin flip, roughly half the time we'll have `rand < 1` and instead we'll `vertexPattern2( )`.  
          

```java
 //Code snippet for random logic to determine which shape is created.
          
   float rand= random(0,2); 
   if(rand > 1){
        vertexPattern1(size, foreground, background);
    }
    else{
        vertexPattern2(size, foreground, background); 
    }

```

###Other Patterns based on i, j index

![](/assets/Screenshot 2017-09-27 19.38.40.png)

###Min( i, j)
The logic for the image above uses the fact that along square shaped sections, like the outer top-row and the left-column both share the feature that the minimum value of the i,j index for each element is 0.

 k = min( i, j); 
 
 ###Max( i, j);
The logic for the image above uses the fact that along square shaped sections, like the outer bottom-row and the right-column both share the feature that the max value of the i,j index for each element is 5.
 
![](/assets/Screenshot 2017-09-27 19.40.34.png)  
  

 
 
 The [lerpColor( ) function](https://kdoore.gitbooks.io/cs1335/content/lerpcolor-and-map.html) can use a factor like k to determine color for each grid cell. 







