#PImageButton

###Class PImageButton
The PImageButton class is a child-class of the Button class.  The extends keyword in the first line of code in the class definition below shows the syntax for defining this class as a child-class of the Button class.  As a child class, PImageButton inherits all properties and methods of the Button class.  

###Over-ride display( ) method


```java

class PImageButton extends Button{
  PImage img;
  
  //constructor
  PImageButton(PImage _p){
       super();
       img = _p; 
  }
  
 // constructor
  PImageButton(float _x, float _y, float _w, float _h, PImage _img){
       super(_x, _y, _w, _h);
       img = _img;
  }
  
  //over-ride display() from base-class
  void display(){
        super.display();
        image(img, x+5,y+5,w-10,h-10);
  }  
}
```
