# Creating Object Instances

###First: Create Class Definition
To create an instance of an object, first we need to have the full definition of the class,  which includes 3 main components:  Instance Variables, Constructors, and Methods.
 

###Second: Create Object Reference-Type Variable
Once we have the class definition, such as our Button class, then in order to create an instance of a class object, we do several things:
1.  **Create a Reference-Type variable:** We need to declare that we will make an object of that specific data-type, so we must create a reference variable that we can use to access (or refer) to our object instance.
    - Button myButton;   //declare a reference-type variable, this can point to a Button object (it can hold the memory address of a Button-type object);
    - The default value for a reference-type variable is 'null'.  
    - null keyword is a literal value that means an  reference-type variable does not currently refer to an object instance. This allows us to test whether or not a reference-variable currently contains a valid memory address of an object.
    - Button myButton; when we first declare an object reference, it is null;
    - myButton = null;  Allows us explicitly set an object reference to null

2. **Call a valid Constructor Method (function) to create an object instance:**
    - We need to use the keyword `new` to call a constructor
    - we need to call one of the constructors we defined in the class.
    - Executing:   new Button() does several things:
        - it creates memory for our object in the 'Heap', the memory place where objects are stored for our program.
        - it executes code in the constructor method, this is a good place to initialize variables for our object
    - We will usually call a constructor using the following syntax:
        - `myButton = new Button()`  - this sets the value of our object reference variable to be the memory address location in the heap where our object data is stored.
        
3. **Use the Object Instance:**  once we have an object reference variable which is pointing to an object instance, *the memory location of our object's data* , now we can call methods of the object using dot notation:
    `myButton.Click();`   or we can modify instance variables `myButton.x = 5;`
4.  **Null pointer exception**: If we try to do step 3 before we've done both step 1 and 2, *we try to use an reference variable to call object methods,....before we have established a connection between our reference variable and an object instance*....then we'll get a `null pointer Exception`.  
5.  **Multiple references to a single object**:  It is perfectly ok to have more than 1 object reference variable `pointing to an object instance`.  This would look like:
    ```
    Button myButton = new Button();  //create reference variable and call constructor 
    Button myButtonPointer = myButton;  // 2 Button reference variables are both `referring` to a single Button object instance.
    
    ```
6.  **Passing Objects into Functions as Parameters**

    When we call a function or a method, if the function has an input parameter which is an object: then the address of the object is passed into the function. So, changes made to the function's local-parameter reference-variable are actually affecting the object, since it points to the same object adddress.  
    
    ```
    //create function that takes an object as input parameter
    void myFunction( Button localButton ){
         localButton.x = 100;
    }
    Button myButton = new Button();
    myButton.x = 5;
    myFunction( myButton ); 
    
    println(myButton.x);  ///myButton.x is now 100, it was modified in the function
    ```

    When this function completes executing, then the local parameter, localButton, is destroyed, so it's no longer pointing at the object.
    
    
    
    
