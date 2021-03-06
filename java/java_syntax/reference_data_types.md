# Object Reference Data Types

#### Primitive Data-types: well-defined size: 

When we covered Functions, we discussed variable scope, we were discussing how **primitive data** type variables are defined as being visible, or available for use by the executing program. **Primitive data type**s are what we've been using so far.`int, float, boolean, char`. The data associated with primitive variables is stored in the program's execution stack, which is where the program's code is located when the program is executing.

## Object Reference-Type Variables: memory address

It is important to realize that when we pass **`object references`** into a function, then any modifications we make to that object will be _persisted_ to the object after the function has finished executing. In this respect, the rules of local and global variable scope don't affect objects, in the same way they have applied to the primitive data-types we've been using. Variables used to refer to objects are called reference-type variables instead of primitive-type variables. We now need a different way imagine the labeled-box that stores our variable's value, instead of a primitive-value being stored in our box, in this case, the address of the place in memory where our object's data is located, is the value that is stored in our 'variable-box'. This address points to a specific address or memory location where our object's data is stored. So, we are passing the _address of an object_ into a function, this is why changes made in a function are persisted to the object.

To declare an Object Reference-Type Variable, specify the **class name to specify the data-type**, then provide a custom variable name.  The object reference variable has a default value of **null** which indicates that the variable does not contain the memory address of a valid object. The object reference variable is initialized by calling a special type of **class method:**  **constructor methods** which have a method name that matches the class name: 

```java
Button myButton; //not initialized has default value of null
myButton = new Button( ); //call a constructor 
```

## null - Uninitialized Reference Variable

```java
Button myButton; //declare an object reference variable
if( myButton == null){
    println("myButton doesn't refer to an object in memory, please initialize before trying to use");
}
//use new keyword and call constructor function 
myButton = new Button( );  //this creates an object and assigns memory address to myButton variable
if( myButton != null){
    println("now it's safe to do button things");
}
```

## Heap: Object Memory-Storage

This difference in memory-storage architecture is partially because objects represent much more complicated data-structures. The memory space for holding object data is called 'the Heap'.  While we never write code to directly access The _**Heap**_ is a data-structure with methods to manage the storing  object data. When the system executes our program, it may not know exactly how much memory space we need for each object that we create. If we create a Menu object, we may choose to have the menu have 3 buttons, we may choose to have it hold 10 buttons, and we might not even decide how many buttons we want in our Menu object, until the program is executing. In that case, we'd be dynamically determining how large our Menu object is, and that could be different each time our program executes.

## Java:  Pass-By-Value

There is a subtle distinction between how objects are passed to a function that can vary between different programming languages. Since Processing is based on Java, we need to understand how Java passes variable values into functions. We have specified that when we are working with objects, which are Reference-types, the variable actually contains the memory-address of the object, and that a copy of the address value is passed into the function. If inside the function we modify the address itself, then we break the connection between the object and variable that was holding the address, so changes would occur on whatever object is now pointed to by the function's local address variable.

