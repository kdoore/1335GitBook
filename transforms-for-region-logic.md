#Transforms for Region Logic

After creating our mini-pattern preview, it should cause us to rethink the complex logic that we've been using for creating regions in our designs. This will begin our transition into object oriented thinking.

###New Idea, Shape Grid-Units: Position with Transforms 

Instead of having complex logic within a single for loop, let's create simple grids and position them using transforms.  This can lead us to simplified logic, which can allow for more complex patterns.  In addition, we can implement logic for layering patterns on top of other patterns to achieve complex designs from simplified logic.  

###2-Dimensional Arrays for Storing our Shapes
We have focused on using 1 dimensional arrays to store our shapes as we've created them.  Now is a good time to consider switching to 2D arrays, as the logic we've been learning can be useful as we store our designs.

###Declare and initialize a 2D array:
int rows= 5 ;
int cols = 5;
PShape[][] shapeGrid; //declare a 2D array
shapeGrid = new PShape[ rows ][ cols ];

###Processing lerpColor( ) Function



