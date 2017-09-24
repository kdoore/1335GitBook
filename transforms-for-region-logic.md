#2D Arrays for Grid Gradient Patterns

After creating our mini-pattern preview, it should cause us to rethink the complex logic that we've been using for creating regions in our designs. This will begin our transition into object oriented thinking.

###New Idea: Position ShapeGrids with Transform Functions 

Instead of having complex logic within a single display-function for-loop, let's create simplified grid modules and position them using Processing's transform functions.  This can lead us to simplified logic, which can allow for more complex patterns.  In addition, we can implement logic for layering patterns on top of other patterns to achieve complex designs from simplified logic.  

###2-Dimensional Arrays for Storing our Shapes
So far, we have focused on using 1 dimensional arrays to store our shapes as we've created them.  Now is a good time to consider switching to 2D arrays, as the logic we've been learning can be useful as we store our designs. 
If we create and store shapes using linear (1D) logic, then we need complex logic to have 2D gradients, however, if we create our and store our shapes as 2D patterns, then  it is easier to incorporate higher level design ideas. 

 ###Diagonal Color Gradients
 ![](/assets/Screenshot 2017-09-24 08.43.41.png) 
 
In the image above, we see a diagonal color gradient in both the foreground and background colors. The logic associated with this can be seen in the image below.  If we define a new variable: `int k = i + j;` , where k is the sum of the i, j index variables, we see that the value of k increases along the grid's diagonal direction.  Then we can use k as a factor to determine the fill color. 

###Color Gradient Logic:
Using the sum of grid indexes for color logic gives us a simple approach to create complex patterns.
    

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

![](/assets/Screenshot 2017-09-24 09.33.22.png)







