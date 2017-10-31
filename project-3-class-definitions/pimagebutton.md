#PImageButton

###Class PImageButton
The PImageButton class is a child-class of the Button class.  The extends keyword in the first line of code in the class definition below shows the syntax for defining this class as a child-class of the Button class.  As a child class, PImageButton inherits all properties and methods of the Button class.  

###Example use:

  

```java
//main tab
  PImage img1 = loadImage( "eraser.png"); //must have image in data folder inside processing project
  
  //can use Button data-type for object reference variable 
  Button imgButton = new PImageButton( btnX, btnY,   buttonSize,buttonSize, color1 ,color2 ,  img1);
  
  imgButton.display();  //overrides Button display() method
  
  //in mouseClicked function
  
  imgButton.clicked( mouseX, mouseY);  //uses Button clicked( ) method

```


###Class Definition Code

```java

//add comments
class PImageButton extends Button {

  PImage img;
  //constructor

  // constructor
  //add comments
  PImageButton(float x, float y, float w, float h, color c1, color c2, PImage img) {
    super(x, y, w, h, c1, c2, "");  //call constructor with empty string for label
    this.img = img;
  }
  
  //over-ride display() from base-class
  void display() {
    super.display();  //call base-class: button display method to create background button
    image(img, x+20, y+20, w-40, h-40);  //adjust as needed
  }

}  //end class PImageButton


```
