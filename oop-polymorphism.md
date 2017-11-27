#Polymorphism

Polymorphism is one of 3 foundational concepts of Object Oriented Programming.  Polymorphism can be translated to mean _many forms_.  In OOP, polymorphism means that one object can be considered to have many forms, specifically, an object from a child-class can be treated as both a base-class object and a child-class object.  So, polymorphism means that child-class objects to be treated as their more general, base-class type, and this reflects our intuition about relationships between real-world objects.  My pet, Charlie, is an instance of a dog object, but he can also be considered as an animal, which would be the more general concept, or base-class concept.  

###Object References
We can create an object reference variable of the base-class type, and this variable can be used to reference either a base-class object, or any object that is of a child-class type.  We can imagine a set of classes, where Animal is the base-class, where Cat and Dog would be child-classes that extend Animal.  Below are examples using default constructors to demonstrate  using base-class object references to refer to child-class object instances.


###Array of base-class object references
```
Animal[] = new Animal[3] //array of base-class object references
Animal[0] = new Animal( ); //base-class object

Dog dog1 = new Dog( );  //child-class object
Animal[1] = new Dog( );  //base-class type object reference, child-class object

Cat cat1 = new Cat( );
Animal[2] = new Cat( );

```

###Over-riding Methods
OOP Polymorphism means that when a child-class object executes a method, then the 'system' will determine whether to execute a child-class method or a base-class method, by examining the child class definition to see if the method has been implemented in the child-class so that it over-rides the base-class method.  Method over-riding allows us to treat objects using the more general, base-class, references, but that the 'system' will determine the run-time type of each object instance, and determine whether a base-class or child-class method will be executed.  

###Object Oriented Design 
Polymorphism should be considered when designing classes with inheritance relationships.  Only methods defined in the base-class can be called on base-class object references, even if the object refers to a child-class object.  Therefore, UML class diagrams provide a graphical representation to aid design and use of OOP classes and objects.
