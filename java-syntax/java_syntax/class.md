# Class

A class provides the specification and definition of properties, constructors, and methods for creating object instances of that class.

> A class is the blueprint from which individual objects are created. [Java Specification (Oracle) ](https://docs.oracle.com/javase/tutorial/java/concepts/class.html)

## Class Definition

A class is created in java by writing code for a class definition. A class definition includes:

* Class name
* Class properties or instance variables
* Class constructor methods
* Class methods

## Creating Objects

It's important to distinguish between a class and an object. An object is created dynamically at run-time; it is considered an object-instance of a class that has been defined in code. To create an object instance, you will use the following syntax:

ObjectType variableName = new ObjectConstructor();

Ball ball1 = new Ball( ); Ball ball2 = new Ball( 10, 10 );

## UML Class Diagram

A UML Class diagram provides a diagramatic representation of the features of a class. In addition, a UML class diagram shows relationships between different classes, such as inheritance and composition.

The UML Class diagram below shows

* class name: Ball,&#x20;
* class properties or instance variables: x, y, size.
* methods (functions): move(), display( )

Some UML class diagrams also show constructor methods.

![](<../../.gitbook/assets/Screenshot 2016-09-16 08.30.08.png>)
