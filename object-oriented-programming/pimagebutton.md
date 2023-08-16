# Child-Class: PImageButton

## PImageButton Class

If we look at the code for the PImage Button below,in the first line, we see the keyword _extends_ which is how we indicate that this class inherits from the Button base class. Then we see that we are able to call the Button base class constructor using the _super_ keyword to call the Button base class constructor `super()`. In addition, we can also use _super_ as a way to call the Button base class methods: `super.display()`. This allows us to first call the Button display method, which gives use the background display of the default Buttons, then we can display the image() to customize the appearance of the PImageButton.

## Class PImageButton

```java
//add comments
class PImageButton extends Button {

  //PROPERTIES

  PImage img;

 //CONSTRUCTORS

  //First line of code executed in a child-class constructor must be a call to the base-class constructor
  PImageButton(float x, float y, float w, float h, color c1, color c2, PImage img) {
    super(x, y, w, h, c1, c2, "");  //call constructor with empty string for label
    this.img = img;
  }

  //METHODS

  //over-ride display() from base-class
  //add comments
  void display() {
    super.display();  //call base-class: button display method to create background button
    image(img, x+20, y+20, w-40, h-40);  //adjust as needed
  }

}  //end class PImageButton
```

## Create a PImageButton Object in Main Tab

The code below shows that we

```java
//main tab
Button pBtn;

void setup(){
  size( 400,400);
  color colorOn = color(250, 50, 100);//purple
  color colorOff = color(250, 50, 50);//dark purple
//declare a PImage object reference variable, initialize using loadImage()
  PImage img = loadImage("pattern1Btn.png");  //this file must be in the project data folder

  pBtn = new PImageButton(20,20,100,100,onColor, offColor, img);  //call PImageButton constructor
} //end setup

void draw(){
  pBtn.display();
}

void mouseClicked(){
  pBtn.clicked( mouseX, mouseY) ;
}
```

## Processing Data Folder

To create a PImage object in the main tab, we must first make sure we have an image that we can use in our project. In order to use any files as data files for our project, we must create a `data` folder inside our current processing project folder. We need to place any images or other resources that we'll use in our projects within this data folder, so Processing knows where to locate these assets and we don't need to specify the file path to this folder.

![](<../.gitbook/assets/Screenshot 2016-02-17 11.59.08.png>)

## Processing PImage

To learn more about how to use PImage objects, refer to the Processing.org [PImage](https://processing.org/reference/PImage.html) Reference. To create a PImage button, we can create a reference-type variable of type PImageButton and then we pass the filename to the PImageButton constructor.

```java
PImage img = loadImage("myImage.png");
pBtn = new PImageButton(20,20,100,100,color(100), color(200), img );
```

## Inherited Method: clicked( )

In the mouseClicked function we need to call the click() method.`pimageBtn.click()`. We haven't explicitly defined the clicked( ) method in the code above because we want to use the Button base-class clicked( ) method. By not redefining clicked( ) in the child class, any child class instances will execute the clicked() method of the Button base class.

## Over-ride Method: display()

In the draw loop we need to call the display method of our pimageBtn: `pimageBtn.display()`. Since we have provided explicit implementation of the display() method in the child class, then when a PImage object instance executes the display( ) method, it is this PImageButton child method that is executed. As discussed above, the code: `super.display()` in the PImageButton class calls the Button base class display() method to draw the background rectangle before drawing the PImage image.

Example Image For ImageButton

![](../.gitbook/assets/pattern1Btn.png)
