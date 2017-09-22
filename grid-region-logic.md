#Transforms for Grid Regions

While we can go down the path of putting our complex pattern logic within a nested for-loop, we'll quickly get overwhelmed trying to organize our logic so it's easy to conceptualize.   

After, stepping back to get an overview of the design challenge, we can try a different approach, and this will lead us toward an object-oriented approach to design our prototyping tool.

![](/assets/Screenshot 2017-09-22 14.46.17.png)

![](/assets/Screenshot 2017-09-22 14.51.04.png)

###Logic for Displaying Patterns in Regions

The code below shows that we can use for-loop logic that looks at the index values: i, j to determine 4 regions where we can display different shapes to develop a more interesting pattern.  

**Region Design Patterns:**
Region1:  Shape1
Region2:  Shape2, in even cells, put Shape1
Region3:  Shape2, in even cells, put Shape1
Region4:  Shape1

**Region Logic:**
Region1: i < rows/2 && j < cols/2
Region2: i < rows/2 && j >= cols/2
Even Cells: (i+j) % 2 == 0 
Region3: i >= rows/2 && j < cols/2
Even Cells: (i+j) % 2 == 0 
Region4: i >= rows/2 && j >= cols/2
 
