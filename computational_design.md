#Parametric and  Computational Design

Wikipedia: 
Parametric design is a process based on algorithmic thinking that enables the expression of parameters and rules that, together, define, encode and clarify the relationship between design intent and design response.[ Wikipedia Link](https://en.wikipedia.org/wiki/Parametric_design)  

Dr. Mihai Nadin was an early proponent of of use of computers as part of the design process.  
>He founded the world’s first program in Computational Design in 1994 at the University of Wuppertal (Germany). Its purpose was twofold: 1. development of a theory of computational design; 2. the design of products and processes through digital means. Currently Mihai Nadin is a professor at the University of Texas at Dallas, appointed to the Ashbel Smith Professorship in Interactive Arts, Technology, and Computer Science. He is director of the Institute for Research in Anticipatory Systems.  [Wikipedia ](https://en.wikipedia.org/wiki/Mihai_Nadin#Computational_design) 

Designing Processes rather than Objects 
>I think that the most interesting shift in recent design experience is that we have passed from designing objects to designing networks and processes.   [Francesco Cingolani](http://ecosistemaurbano.org/english/francesco-cingolani-eu-collaborators/)

###What is the difference between “parametric design” and “computational design” ?
>I don’t know. “Computational design” refers to the use of computers and mathematical approach to the generation of geometries, objects and architecture. “Parametric design” is about using parameters to design things. It means that if parameters changes, the result change. Regardless of which expression is the best, what interests me the most is the idea of focusing on design process instead of designed objects.  [Francesco Cingolani](http://www.immaginoteca.com/parametric-vs-computational-design/)

###Programming as a Design System
 In the introduction to his graduate course: Programing Design Systems, Rune Madsen provides an excellent in-depth article on the [History of Design Systems](http://printingcode.runemadsen.com/lecture-intro/) by Rune Skjoldborg Madsen


###Computational Design Spaces
[Articles by Danil Nagy](https://medium.com/generative-design/introduction-to-computational-design-6c0fdfb3f1)
Computational strategies for defining design spaces
Based on our discussion of computer programming so far, we can think of a number of strategies for defining our design spaces computationally:
Morphological control through continuous variables
State-change control through discrete variables
Recursive control through functions and rule sets
Behavioral control through object-oriented programming
![](https://miro.medium.com/max/1200/1*B5dB34LLxSgGYCI14faULA.png)


###Parametric Design for our Projects
In our recursive pattern design, we have specified that the geometry of our pattern is based on a single parameter: length.  We have specified all of the vertex points for our design using only length (or length/2), where we are assuming that our pattern has a central vertex as (0,0), and that all other vertices are defined relative to this central vertex.  This allows us use our function: vertexPattern( float length) to create a drawing application using a parametric design approach. We have designed our function so that it has a parameter that we can easily map to some user input, to produce variations in the pattern's design.  In the next versions of the project, we will design an application which gives our users the interactive-control to modify parameter of design patterns to create unique graphical designs.  We can also modify other features of the design, such as hue, saturation, brightness of the pattern based on user interactions.  To do this, we need to create a connection between user interaction and the geometry and color of the patterns they create. 

###Map Function to Control Hue, and other features
Below is a short processing program where we are using HSB colormode, the processing map() and dist() functions to create a simple application that has user mouse movement mapped to various geometric and color properties to create an interactive design experience.



In the code below, we are calculating values for hue, saturation and brightness using a mapping between the mouse position and a range of values for hue or saturation or brightness.  
For example, in the code below, we are using the current mouse X coordinate: mouseX, and we're using that to give us a value, we're calling it hueVal, that is in a range from 100 to 200.  Then we use this to set the fill for drawing something in our program.  In the program below, we're doing a similar mapping to control several aspects of the design based on the user's current mouse position. 

```float hueVal = map( mouseX, 0, width, 100, 200);```

Full Program:
```
void setup(){
  size(800, 600);
  colorMode(HSB);
  background(255);
}

void draw(){
   if(mousePressed){
     drawPattern();
   }
}

void drawPattern(){
  ////local function variables
  float hueVal = map( mouseX, 0, width, 100, 200);
  float satVal = map( mouseY, 0, height, 50,255);
  float distance= dist( mouseX, mouseY, width/2, height/2);
  float size= map( distance,0, 500, 120,12);
  float brightVal=map(distance, 0, 200, 255,200); ///darker towards edges based on distance
  float someRandVal=random(-5,10);
  
  fill(hueVal, satVal, brightVal);  //use mapped values
    
  translate(mouseX, mouseY);  // move origin to mouseX,mouseY
    ellipse(0,0, size+someRandVal, size-someRandVal);
  resetMatrix();  //reset origin 
}

```

