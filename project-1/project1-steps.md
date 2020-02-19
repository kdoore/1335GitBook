# Project1-Steps

### Conceptual Art to Express Emotion / Energy 

### **Step 1: Determine Emotions to express:**

See [Models of Emotion: ](modeling-emotions.md), Concept Maps, [Mental Models](https://en.wikipedia.org/wiki/Mental_model)

**Create Personal Situation Concept Map.** Select a personal situation that has an associated range of positive and negative emotions. Sketch a concept-map to brainstorm the concepts and emotions associated with your situation.

* Divide your concept-map sketch into 2 regions:  Negative, Positive
* Put 'Situation' as the center concept \( no need to provide specific details about situation \)
* Add associated concepts to negative or positive sides
* Add emotions to each side, position the emotions to indicate the strength of emotion - with the strongest emotions located at the outer edges of the regions, neutral emotions near the central dividing line 
* Result: Select at least 5 emotions to represent in your artwork, list these along the bottom of your concept map.
* **Project Planning Document**
  * Define variables: 
    * region colors \( minimum of 4 custom colors required \)
    * PShape length ranges \(minSize, maxSize\)
  * Main Emotions: ordered list of 5 emotions or feelings
*  **Planning document as a guide to complete the logic** to determine parameters for the RecursivePattern functions, for each region..
  * **Negative - region:**  0 &lt; mouseX &lt; balancePoint
  * **Positive - region:** balancePoint &lt; mouseX &lt; width

## Code Structure:  Function Signatures:

```java
//Helper Functions will call Recursive pattern functions
//Contain map and lerpColor logic
void positivePattern( float balancePoint, int mx)
void negativePattern( float balancePoint, int mx)


//recursivePattern functions with parameters
//Use size, minSize for termination 
void posRecursivePattern(float size,  color c1  )
void negRecursivePattern(float size,  color c1 )


//Custom PShape functions - use vertex points
//minimum of 8 vertex points per function
//one shape must have a cutout - inner contour
PShape customPosShape(  float len, color c1)
PShape customPosShape(  float len, color c1)
```

### **Step 2:  Region Logic: PositivePattern, NegativePattern:**   

#### **Helper functions: with logic for each region to determine color, size based on mouseX position relative to the balancePoint position.**

```java
//determine current size, color: gradients across the positive region
void positivePattern(  float balancePoint, int mX){
   
  color cPos1 = color( 230, 100, 100); //purple
  color cPos2 = color( 80, 100, 100); //lime
  
  //define curColor based on mX relative to balancePoint
  float fraction = map( mX, balancePoint, width, 0.0, 1.0);
  color curColor = lerpColor( cPos2, cPos1, fraction); //fraction varies beteween 0.0, 1.0
  
  float curSize = map( mX, balancePoint, width, minSize, maxSize );
  
  //Call Recursive Function
  posRecursivePattern( curSize, curColor);
  }
```

**float curSize** - determined by region and mouseX

* use map\( \) to determine curSize for each region

`float curSize = map( mX, balancePoint, width, minSize, maxSize );`

**colors:  Define 2 colors per region: cPos1, cPos2** - determined by region and mouseX

* use map\( \) to determine color gradient fraction

`float fraction = map( mX, balancePoint, width, 0.0, 1.0);` 

* use lerpColor\( \), fraction to determine color for current mouseX position

`color curColor = lerpColor( cPos2, cPos1, fraction); //fraction varies beteween 0.0, 1.0`

* you must determine logic for negative region

#### Random Pops of Color - Optional

* Optional:  determine probability for random pop of color, this can be set for each region, or can vary within each region using map\( \) to set value of float randPopColor

  `float randPopColor = map( mouseX, balancePoint, width, 0.3, 0.6); positive`

* you can add small variation in hue

**Call Recursive Function**

`posRecursivePattern( curSize, curColor);`

###  **Step 3:  Recursive Functions:**

```java
     //Draws a single motif - nested size and color gradient
void posRecursivePattern( float size, color c1){
  //termination test
  if(size < minSize){
    return;
  }
  //task
  float fraction = map( size, minSize, maxSize, 0.2, 1.0); //may want to customize
  color curColor = color( hue(c1), saturation( c1), brightness(c1)*fraction);
  PShape s1 = customPosShape( size, curColor); //test the shape
  shape(s1,0,0); //render the shape at the origin
  
  //recursive call
  posRecursivePattern( size * 0.8, c1); 
  //task - with reversed stacking - mirror across origin
  pushMatrix();
  scale( -1, -1);//mirror across the x, y axis (origin)
  shape( s1, 0, 0);
  popMatrix();
}

```

#### Termination Condition

`if(size < minSize)  
{ return; }`

#### Recursive Function Task: Create, Render Custom PShape

Use map function to determine how brightness should change for each individual PShape layer.  Local variable: fraction changes as size changes, with the smallest size corresponding to the smallest fraction value: 0.2.  Adjust as needed.   

`float fraction = map( size, minSize, maxSize, 0.2, 1.0);   
color curColor = color( hue(c1), saturation( c1),brightness(c1)*fraction);   
PShape s1 = customPosShape( size, curColor);    
shape(s1,0,0); //render the shape at the origin`

#### Recursive Function Call

You **must modify  size for each recursive call**, this can be done when setting the input parameters as below. 

`posRecursivePattern( size * 0.8, c1);` 

### Step 4. Custom PShapes: Specify Vertex using len  parameter

```java
//Draws a single shape
PShape customPosShape(  float len, color c1){
  PShape s; //declare our first object-type variable //heap - object memory
  fill( c1);//attempt to set color for the shape
  s = createShape( );//initialize our shape
  s.beginShape();
  s.vertex( 0,0  ); //1 x, y points
  s.vertex(.5 * len , 0 ); //2
  s.vertex(len , .5* len ); //3
  s.vertex(.5 * len , len  );//4
  s.vertex( 0,  .5* len ); //5
  s.vertex( 0, 0 ); //6
  
  s.beginContour(); //make internal cutout 
  s.vertex( len*.25,len*.45); //inner cutouts - point 5
  s.vertex(len*.6, len*.6);  // 
  s.vertex( len*.45, len*.25); // 
  s.vertex(0,0);
  s.endContour(); //end internal cutout

  
  s.endShape();
  //shape( s, 0,0);  //render to the canvas
  return s; //return the PShape
  
}
```

