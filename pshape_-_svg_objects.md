
# PShape Objects

The [Processing website](https://processing.org/reference/PShape.html) has a good [tutorial about PShape](https://processing.org/tutorials/pshape/) objects, so it's advisable that you
review that tutorial in order to have a basic understanding of `PShape` objects.  The idea is
that `PShape` allows us to create geometric primitives that we can use as objects.  There are 
a variety of ways to use PShape, let's start by creating simple Rectangle PShape object. 

###Processing Primitives
The easiest way to create a PShape object is to use the Processing Primitives mode, this allows us to create a PShape object using processing shape primitives:

```java

PShape s = createShape(RECT, 0,0,40,50);
///then to display it
s.setFill(color(255, 0, 0));  //set color to red
shape(s, 20,20);  //specify x, y location
```

###Types of PShapes:
There are actually 3 different types of Processing PShape objects: one type is created by loading a .svg image file. In that case, we initialize the PShape object using the LoadShape function, example:
PShape s = loadShape("myImg.svg");


The other type of PShape object is created using the Processing primitive shape modes: RECT, etc, or by defining a series of verticies. For these types of PShapes, we initialize the PShape object using the CreateShape function, example:
PShape s = createShape(RECT, 0,0,40,40);
When we want to use these PShapes to create a drawing pattern, then we will want to be able to modify the size, shape, and styling of the PShape object. However, for each different type of PShape object, we need to use slightly different syntax to modify these things. So, can we create a generalized PShapePattern class that will allow us to use either type of PShape object?


###PShape Fill Options
For each different type of PShape, either vertex pattern, processing primitive, or loaded external .svg file, there are quite a few ways that we can modify the color of a PShape object. 
The code below shows 3 ways to set the fill of a vertex type PShape object.  Copy the code and try the various methods.

**PShape using vertex( )**
```java
void setup(){
size( 400,400);
float len=100;
color red = color(255,0,0);
color blue = color( 0,0,255);
color green = color(0,255,0);
//fill(green); // using fill before creating the shape
PShape s2 = createShape();
s2.beginShape( );
//s2.fill(color( 255,0,0)); //after calling beginShape() the object,specify fill using color
s2.vertex( 0, 0);
s2.vertex( len * .5, len * .5);
s2.vertex( len, len);
s2.vertex( len * .5, len);
s2.vertex( 0, len);
s2.endShape( CLOSE);
//s2.setFill( blue); //can change color once endShape( ) has been called
shape( s2, 200, 200);
}
```

###Stars

In the Processing `PShape` tutorial, the authors create a Star class, and they use the createShape(), beginShape()
and endShape() functions, along with a list of vertices in the Star constructor to create the geometry for the
Star object.  

However, they go on to describe a subtle concept; the idea of creating the star geometry one time in
the main setup() function, and then passing that PShape object as an input parameter to the Star constructor.  This 
can cut down on rendering costs, where Processing can essentially memorize the geometry of the single PShape object, 
rather than having to render the geometry for each one.  

For now, let's ignore these suggestions, and we'll create the geometry in the Star constructor function.  
Below are snippets of code for the Star class, where it inherits from the Drop class.  

For our current version of the RainDrop game, the Drop class does not inherit from any other class::

	class Star extends Pattern{  
		PShape s;
		
		Star(){  // constructor lets us set the x-position
			super();  // call the Drop constructor as the first line of code
		
		// First create the shape
			s = createShape();
			s.beginShape();
			// You can set fill and stroke
			s.fill(102);
			s.stroke(255);
			s.strokeWeight(2);
			// Here, we are hardcoding a series of vertices
			s.vertex(0, -50);
			s.vertex(14, -20);
			s.vertex(47, -15);
			s.vertex(23, 7);
			s.vertex(29, 40);
			s.vertex(0, 25);
			s.vertex(-29, 40);
			s.vertex(-23, 7);
			s.vertex(-47, -15);
			s.vertex(-14, -20);
			s.endShape(CLOSE);
			}// end constructor
            
        void display(){
             shape(s, 0,0);  //display at origin
        }
		}  //end Star Class
	
The code above is taken directly from the Processing `PShape` Tutorial, except that we've made the
Star class a child class of the Drop class. 

Because the Star class inherits from the abstract Pattern class, we don't need to explicitly
declare most of the instance variables.  However, notice that in the first line of 
code in the constructor that we're calling ``super()``, this is the Drop class default constructor. 

Shiffman notes in the `PShape` Tutorial that by default, a PShape geometry is defined relative to the canvas origin (0,0). 
Therefore, he notes that it's we'll almost always use ``pushMatrix()``, ``popMatrix()``, and ``translate()`` in order to locate
our PShape objects on the canvas.

So, to write a ``display()`` method for our Star, we need to remember to translate the origin of the canvas
to the x,y coordinates of our shape before displaying using the `shape()` function.  Here's a display method that
also lets us set the color of the PShape object::
```
	 void display(){
		pushMatrix();
		translate(x,y);    //x,y were given default settings
  		s.setFill(color(0,200,127));   //we can change the fill color here if we want
		shape(s,0,0);
		popMatrix();
        }
  ```
  
If we want to determine where the center of the PShape is, what code can we write?
The easiest thing to do is to note that we've translated the origin to the x,y position, so
if we create an ellipse at (0,0) then we'll be able to observe where the center is. 

###PShape using SVG Image File


Another way that we can use PShape is to load an .svg file.  There are may sources for .svg files, for
this project, I'm using an svg file from `The Noun Project`.  This site has lots of .svg icon files
that are free for use if you provide proper attribution for the designer of the .svg file.  I'm using
an .svg file of a monster designed by: Joel McKinney at http://thenounproject.com/ .   Below is the monster .svg file.  We can see that 
the image has a text component where the designer's name is listed.  While we need to provide credit to 
the designers in our programs, we need to remove that text in order for this .svg file to work in our
programs. 

![](/assets/Screenshot 2017-04-03 07.42.40.png)

###SVG Fill, Stroke
For our project, we will be modifying the fill property of the SVG object, so you will want to select an SVG object that has a fill property that can be modified, some SVG objects use only stroke.  If you want to use an SVG object with Stroke, then you'll need to change the PShapePattern project code to integrate Stroke modification code.

 

###Edit SVG Files

There are 2 ways that we can edit .svg files.  Since .svg files are a standardized data format file
that list vertices for geometry and font elements, we can open the files in either a vector software
system like Adobe Illustrator, or Inkscape.  We can also open the files in any text editor like notePad
or textEdit. If we open the file in a text editor, then we need to go to the bottom of the file and 
find the ``<text> </text>`` content section.  We need to carefully select this content from the opening tag
to the closing tag, and the delete that content, being careful not to delete anything else.  In addition,
if we look at the .svg file, we can determine the width and height of the object, in addition to other 
image details.  Below is the .svg code for the image above::



So, delete the <text> </text> line in the code above, however, make sure not to delete the closing </svg> tag. Also, 
in the first line of code, if the view box is significantly different than the width and height, which are usually
100px by 100px, then this can cause problems. You will probably want to pick a different image. 

In order to use an svg file for a PShape object, it's necessary to use the following syntax in 
order to load the image.  

	1.  The .svg file must be put inside a folder named: "data", inside your project sketch folder
	2.  PShape s= loadShape("seaHorse2.svg");  // this loads the image 
	3.  shape(s, x, y, width, height) ;  //this is used to display the svg.
	
###SVG Origin

With SVG files, the x,y position refers to the top left corner of the svg file.  If you open the
svg file in a text editor, you can read the width and height dimensions of the svg.  Those can help us
when we try to determine the bounding box for collision detection.  Below is the display function 
that is overriding the default style of the svg to allow us to reset the fill color.  Below that I've
added a rectangle to show the bounding box.  Since we're using translate(x,y) so that we've moved the 
canvas origin to the svg corner point, then we'll draw the rectangle at (0,0).::

	void display(){
		pushMatrix();
		translate(x,y);
		s.disableStyle();  // Ignore the colors in the SVG
		s.setFill(color(255,0,0));   // Set the SVG fill to red
		stroke(55);          // Set the SVG fill to gray
		shape(s,0,0,sWidth,sHeight);
		noFill();
		rect(0,0,sWidth,sHeight);  //bounding box 
		popMatrix();
		}
		

