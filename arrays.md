#Arrays

Arrays are an data-structure that can hold multiple values.   We can consider an array to be a list, which can hold values.  We can also consider arrays as multi-dimensional data structures, a 2D array is like a grid, a 3D array can be considered a cubic structure...etc.  

Arrays are objects in java, so we'll start to learn how to work with objects as we learn to work with arrays.

###Declare an Array
When we want to create an array, we need to learn the unique syntax that java uses for arrays.  To declare an array, we start by declaring the type of data that we want to store in the list, then we use brackets to indicate that we want an array of these values. To initialize the array object we use the ``new`` keyword to indicate that we're creating a java array object, then we must specify the number of elements in our array.  The code below shows how to declare and initialize the array structure for several different types of data.

```java
int[ ] myInts; //declare
myInts = new int[10]; //initialize array of 10 intgers

float[] myFloats = new float[20]; //

int numShapes=10;
PShape[] shapes = new PShape[numShapes]; 


```
###Initialize Array Elements
Once we have our array, which we can think of as an n-item long collection of adjacent containers, then we need to put items in our containers.  If we think of a 1 dimensional array as being like a train, then each train car are the array elements, and we can consider that these individual containers can store a single data item. 

We use `bracket` notation to access each element in the array - inside the brackets we put the index of the item we want to access or modify - array indexes start at 0, the last item in an array has an index equal to arrayLength-1;

  ```java

myInts[0] = 5; //assign 5 to the first array element
myInts[9] = 50; //assign 50 to the last array element
```

Typically we'll use a `for-loop` to access items in an array...where we use the loop's count variable to access each item in the array sequentially.  


