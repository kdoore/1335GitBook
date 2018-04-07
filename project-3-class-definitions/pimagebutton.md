#PImageButton

###Class PImageButton
The PImageButton class is a child-class of the Button class.  The extends keyword in the first line of code in the class definition below shows the syntax for defining this class as a child-class of the Button class.  As a child class, PImageButton inherits all properties and methods of the Button class.  

###Example use:
To use the PImageButton class, you must first have an image in your project folder that you can use for displaying on the button.  You must create a new folder inside your project folder with the name: data.  See image below, which shows that 2 images have been added to the newly created data folder inside the project's sketch folder.

![](/assets/Screen Shot 2018-04-07 at 3.08.50 PM.png)  

The images were created by taking screenshots of the canvas after the patterns had been drawn using the mouse.

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

  //PROPERTIES
  
  PImage img;
  //constructor

  //CONSTRUCTORS
  
  //add comments
  PImageButton(float x, float y, float w, float h, color c1, color c2, PImage img) {
    super(x, y, w, h, c1, c2, "");  //call constructor with empty string for label
    this.img = img;
  }
  
  //METHODS
  
  //over-ride display() from base-class
  //add comments
  void display() {
    super.display();  //call base-class: button display method to create background button
    image(img, x+10, y+10, w-20, h-20);  //adjust as needed
  }

}  //end class PImageButton

```
**PImageButtons shown on the Drawing Application**
You can adjust the dimensions of the image in the display( ) method in the PImageButton class, depending on the size of your buttons.  The dimensions used in the code above work well for a button that is 100 px x 100 px.

![](/assets/Screen Shot 2018-04-07 at 3.13.55 PM.png)