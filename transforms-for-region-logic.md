#Transforms for Region Logic

After creating our mini-pattern preview, it should cause us to rethink the complex logic that we've been using for creating regions in our designs. This will begin our transition into object oriented thinking.

###New Idea, Shape Grid-Units: Position with Transforms 

Instead of having complex logic within a single for loop, let's create simple grids and position them using transforms.  This can lead us to simplified logic, which can allow for more complex patterns.  In addition, we can implement logic for layering patterns on top of other patterns to achieve complex designs from simplified logic.  

###2-Dimensional Arrays for Storing our Shapes
So far,we have focused on using 1 dimensional arrays to store our shapes as we've created them.  Now is a good time to consider switching to 2D arrays, as the logic we've been learning can be useful as we store our designs. 
If we create and store shapes using linear (1D) logic, then we need complex logic to have 2D gradients, however, if we create our and store our shapes as 2D patterns, then  it is easier to incorporate higher level design ideas. 

 ###Diagonal Color Gradients
 ![](/assets/Screenshot 2017-09-24 08.43.41.png) 
 
In the image above, we see a diagonal color gradient in both the foreground and background colors. The logic associated with this can be seen in the image below.  If we define a new variable: `int k = i + j;` , where k is the sum of the i, j index variables, we see that the value of k increases along the grid's diagonal direction.  Then we can use k as a factor to determine the fill color. 
For example:  `fill( 150 + (k * 10)); ` 

###Gradient Logic:
    

```
      int k= i + j;
      fill( 150 + k *10);
```




![](/assets/Screenshot 2017-09-24 09.00.41.png)

###Odd-Even Gradient Logic



```
      int k= i + j;
      if(k % 2 == 0){
      fill( 100 + k *10);
      }
      else{
        fill(240);
      }
```


      
      
![](/assets/Screenshot 2017-09-24 09.08.55.png)



###Declare and initialize a 2D array:
int rows= 5 ;
int cols = 5;
PShape[][] shapeGrid; //declare a 2D array
shapeGrid = new PShape[ rows ][ cols ];

###Processing lerpColor( ) Function



