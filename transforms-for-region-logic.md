#2D Arrays for Grid Gradient Patterns

After creating our mini-pattern preview, it might inspire us to rethink the complex logic that we've been using for creating regions in our designs. This will begin our transition into object oriented thinking.

###New Idea: Position ShapeGrids with Transform Functions 

Instead of having complex logic within a single display-function's for-loop, let's create a set of simplified grid modules and position them using Processing's transform functions.  This can lead us to simplified logic, which can allow for more complex patterns.  In addition, we can implement logic for layering patterns on top of other patterns to achieve complex designs from simplified logic.  

![](/assets/Screenshot 2017-09-24 13.42.33.png)
###1-Dimensional Arrays - Design Limitations
As seen in the image above, when we have a linear ordering for our colors (1-Dimensional array), then when we display those in a grid we see this linear ordering, which we perceive as rows of colors. This is a problem if we want more complex color relationships between neighboring items.

###2-Dimensional Arrays for Storing our Shapes
Now is a good time to consider switching to 2-Dimensional arrays to store our modular design units. 
If we create our and store our shapes using a 2-Dimensional data-structure , then we can store higher-order relationships between our design units, such as 2-D color gradients. 

###Diagonal Color Gradients
![](/assets/Screenshot 2017-09-24 08.43.41.png) 
 
In the image above, we see a diagonal color gradient in both the foreground and background colors. The logic associated with this can be seen in the image below.  If we define a new variable: `int k = i + j;` , where k is the sum of the i, j index variables, we see that the value of k increases along the grid's diagonal direction.  Then we can use k as a factor to determine the fill color. 

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
We can use the Processing random(min,max ) function to simulate random events. We define and initialize a random variable: `rand` that will be assigned a decimal value between 0.0 and 2.0.   We determine that if `rand > 1`, then we `createShapeOne( )`, like a coin flip, roughly half the time we'll have `rand < 1` and instead we'll `createShapeTwo( )`.  
          

```java
 //Code snippet for random logic to determine which shape is created.
          
   float rand= random(0,2); 
   if(rand > 1){
        createShapeOne(size, foreground, background);
    }
    else{
        createShapeTwo(size, foreground, background); 
    }

```











