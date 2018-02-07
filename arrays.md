#Arrays

Arrays are an data-structure that can hold multiple values.   We can consider an array to be a list, which can hold values.  We can also consider arrays as multi-dimensional data structures, a 2D array is like a grid, a 3D array can be considered a cubic structure...etc.  

Arrays are objects in java, so we'll start to learn how to work with objects as we learn to work with arrays.

###Object-Reference Data-Type
Since Arrays are java objects, they are a Reference data-type, this means that the array's name variable actually contains a reference, or pointer, to the location in heap memory space where the array's data is stored as contiguous items.  

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

Typically we'll use a `for-loop` to access items in an array...where we use the loop's count variable to access each item in the array sequentially. Often we'll use the loop count variable as part of the expression to initialize arrays of numbers.  


```java
for( int i=0; i < myInts.Length; i++){
  myInts[i] = i * 10;  
}
```
##2 Dimensional Arrays
2 Dimensional arrays work well as a data-structure for 2-Dimensional data, such as data associated with a grid structure.

Syntax:

When creating a 2 dimensional array, it is customary to have the first bracket index represent the rows, with the j index representing columns.  A for-loop is usually used to step through each element in the collection, where intMatrix[i][j]  refers to a single array element in the i'th row and j'th column position.

```java

  int rows = 5;
  int cols = 4;
  int size=60;
  
  int[][] intMatrix ;  //declare 2D array of integers
  intMatrix = new int[rows][cols]; //initialize 
  
  //nested for loops to access each element
  for ( int i=0; i< rows; i++) {
    for ( int j=0; j<cols; j++) {
      int k=  i + j;  //create a variable to use for fill logic
      intMatrix[i][j] = k; //store this value for each cell
      fill(100+(k*30));  //set fill based on k value
      rect( i* size, j * size, size, size);
     
    }
  }
```

![](/assets/Screenshot 2017-09-28 13.42.54.png)

###Arrays as Function Input Parameters
When we pass array objects into functions, we're actually passing the memory address of the array into the function, so changes made to an array's elements within a function are persisted to the array after the function completes execution.

In the code example below, we declare and initialize a 1 dimensional array of integer values. The array is passed as an input parameter into the function: initializeVals, where each element in the array is initialized to the value of initVal, which in this case is 12. In the second function, modifyOneVal, both input parameters are integers, not objects, so only a copy of the parameter's value is passed into the function. This is referred to as pass by copy. In the case of the Array object, the address of the array is passed into the function, so the function modifies the original array object. 

```java

int[] intVals = new int[10];

//call function, pass intVal array as function input: value
initializeVals( intVals, 12 );
println( "intVal0: " + intVals[0] ); //intVal0: 12

//call function, pass one array element, as function input: int value, the array element value is not modified, 
//only a copy of the integer value is passed to the function.  
//This function DOES NOT actually modify the value of this array element.

modifyOneVal_Useless( intVals[0], 13 );
println( "intVal0: " + intVals[0] ); //intVal0: 12

//function definitions below

void initializeVals( int[] intArray, int initVal ){
for( int i=0; i< intArray.length; i++){
intArray[i] = initVal;
}
}

void modifyOneVal_Useless( int val1, int val2){
val1 = val2;
}


```

