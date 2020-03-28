# Class Example Code

Here is some example code similar to what was done in class.

```java
//Example Class Code 
//Arrays:  Declare, Initialize array, initialize array elements
//Object reference variables -null, or contain a valid memory address to object data in the heap
//Functions: primitive vs object input parameters, return values
//Random - for coin flip logic 

void setup(){
  int num=5;  

  int result = DoSomething( num );  //using the value returned from a function
  //copy of num variable's value ( 5 ) passed into the function
  //num variable not changed by function call
  println("num, result " + num + " , " + result);

  int[] myArray; //Declare the array - has a value of null
  int[] myArray2; //Declare another array - has a value of null

  myArray = new int[ 20 ]; //initialize the array - now variable contains valid memory address
  myArray2 = myArray;  //2nd object reference variable pointing to same memory location

  myArray[0] = 10;  //initialize first element using bracket notation
  myArray2[0] = 15; //change value using other object reference variable
  println( "Array value changed " + myArray[0]);

  //Use a loop to initialize the elements of the array
  for ( int i=0; i < myArray.length; i++){
    myArray[i] = (int) random(0,2); //flip a coin
    println("random value myArray[i] " + myArray[i]);
   }

  DoSomething(myArray[0]); //input parmater is an int, pass in a copy of the value 
  println( "initial Array value " + myArray[0]);

  //Function input value is the memory address of the array
  //so changes to the array in the function are persisted
  //to the array after the function is done executing
  DoArraySomething( myArray );
  println("after function myArray[0] " + myArray[0]); //first array element value was permanently changed in the function call

   } //end setup

//Function that takes an array as an input parameter
void DoArraySomething( int[] list ){ //input parameter is the memory address of the object
  list[0] = 10; //actually changes value in the original array
}

//Function that has an integer input parameter
int DoSomething( int val ){ //val is a local variable
  val = val + 10;  //changing the value of local variable does not change the original variable used in the function call
  println("val " + val);
  return val;
}
```

