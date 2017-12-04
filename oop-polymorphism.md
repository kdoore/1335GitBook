#Polymorphism and Object Oriented Design

Polymorphism is one of 3 foundational concepts of Object Oriented Programming.  Polymorphism can be translated to mean _many forms_.  In OOP, polymorphism means that one object can be considered to have many forms. An object-reference of the base-class type can refer to either a base-class object or a child-class object.  Another way to consider this is that when we have a collection of similar objects, where we refer to them with the more generalized format (base-class type object-reference variable), that variable can refer to any of the child-class objects.

In the example below, this is intuitive for us:  a dog is an animal, a cat is an animal, an animal is an animal.  However, a dog is not a cat, and we can'd force some instance of an animal to be strictly a cat, we would expect this to cause errors as in the example code below.

```java

Animal[ ] animals = new Animal[3];
animal[0] = new Dog();
animal[1] = new Cat();
animal[2] = new Animal( );

Cat cat = new Cat( );
cat = new Dog( ); ///this will cause an error
cat = new Animal( );  ///this will cause an error
```

So, polymorphism means that child-class objects can be to be treated as their more general, base-class type, and this reflects our intuition about relationships between real-world objects.  My pet, Charlie, is an instance of a dog object, but he can also be considered as an animal, which would be the more general concept, or base-class concept.    

###Object References
We can create an object reference variable of the base-class type, and this variable can be used to reference either a base-class object, or any object that is of a child-class type.  We can imagine a set of classes, where Animal is the base-class, where Cat and Dog would be child-classes that extend Animal.  Below are examples using default constructors to demonstrate  using base-class object references to refer to child-class object instances.  It is important to note that the reverse is not true, you can not use an object-reference of the Child-class type to refer to a base class object.


###Array of base-class object references

```java
Animal[] animals= new Animal[3] //array of base-class object references
animals[0] = new Animal( ); //base-class object

Dog dog1 = new Dog( );  //child-class object
animals[1] = new Dog( );  //base-class type object reference, child-class object

Cat cat1 = new Cat( );
animals[2] = new Cat( );

//IMPORTANT:  Note that these will cause errors:
cat1 = animals[0];  //child-class reference-type, base-class object

cat1 = dog1; //child class reference-type

```

###Over-riding Methods
OOP Polymorphism means that when a child-class object executes a method, then the 'system' will determine whether to execute a child-class method or a base-class method, by examining the child class definition to see if the method has been implemented in the child-class so that it over-rides the base-class method.  Method over-riding allows us to treat objects using the more general, base-class, references, but that the 'system' will determine the run-time type of each object instance, and determine whether a base-class or child-class method will be executed.  If a method has not been over-ridden in a child class, the child-class object can still call any method specified in the base-class, the child-class 'gets' everything in the base-class 'for free' when it extends the base-class to become a child-class.

###Object Oriented Design 
Polymorphism should be considered when designing classes with inheritance relationships.  Only methods defined in the base-class can be called on using base-class object references, even if the object refers to a child-class object.  Therefore, UML class diagrams provide a graphical representation to aid design and use of OOP classes and objects.

###UML Diagram of Inheritance Relationships

![](/assets/Screen Shot 2017-11-30 at 2.09.48 PM.png)

The diagram above shows a base-class: Creature, and 3 Child classes:  Zombie, Cat, Fish 

When creating object reference variables, we specify the data-type of the variable, and this impacts the methods that can be called for the object.  

Example 1:  **Base-class object-reference variable:**

    Creature creature = new Fish( 10, 10, f ); 

This object can call any methods that are specified in the base-class.

    creature.display();
    creature.move( );
    creature.attack( creature );  
    
This object can not call any methods that are not specified in the base-class, even if they are specified in the child-class for the object's actual data-type:

    //this will cause an error:
    creature.glubGlub( );
    
Example 2: ** Child-class object-reference variable:**

     Fish fish = new Fish( 10, 10, f);
     
 This object can call any methods specified in either it's base-class, or it's own class (Fish)
 
 
     fish.attack( fish );  //no error doing this
     fish.glubGlub( );
     
 ###Object Oriented Design - Add methods to the base-class to provide access to specialized behavior in child-classes.
 When designing classes, as in the example above, we should identify any specialized behavior that will be exhibited by any child-class and create a method in the base-class that represents the generalized behaivor.  
 
 Example:  We have a child-class: Fish, where the fish has a specialized behavior:  glubGlub( ).  Let's assume that can be considered as a more generalized concept:  makeNoise( ), where other child classes might also share this behavior.  If we define the method:  makeNoise( ) in the base-class, then, within the Fish class, we can over-ride makeNoise( ), and call the glubGlub( ) method within makeNoise( ).  Then any base-class object can call makeNoise( ), if the object happens to be a Fish, child-class object, it will have it's glubGlub( ) behavior executed.

```java
//within the Creature class: provide makeNoise( ) 
 
 void makeNoise( ){
     println("some creatures will make special noises by overriding this method");
 }

```

 
```java
//Within the Fish class: over-ride makeNoise( )
void makeNoise( ){
     this.glubGlub( );
 }
```
The image below shows an improved object-oriented design, so that all methods implemented in the base-class can be called by an object with a base-class type reference variable, and if the object is a child-class object, it'll have specialized behavior because it has provided an over-ride for methods where it has special logic to be executed
 
 ![](/assets/Screen Shot 2017-12-04 at 10.38.18 AM.png)
    
