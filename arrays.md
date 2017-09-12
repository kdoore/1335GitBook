#Arrays

Arrays are an data-structure that can hold multiple values.   We can consider an array to be a list, which can hold values.  We can also consider arrays as multi-dimensional data structures, a 2D array is like a grid, a 3D array can be considered a cubic structure...etc.  

Arrays are objects in java, so we'll start to learn how to work with objects as we learn to work with arrays.

###Declare an Array
When we want to create an array, we need to learn the unique syntax that java uses for arrays.  To declare an array, we start by declaring the type of data that we want to store in the list, then we use brackets to indicate that we want an array of these values. To initialize the array object we use the ``new`` keyword to indicate that we're creating a java array object, then we must specify the number of elements in our array.

```java
int[ ] myInts; //declare
myInts = new int[10]; //initialize array of 10 intgers

float[] myFloats = new float[20]; //

int numShapes=10;
PShape[] shapes = new PShape[numShapes]; 


```

