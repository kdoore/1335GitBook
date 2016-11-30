# PShapeAgent With PShape Groups


PShape objects have the capability to have a group of PShape objects which comprise a group, this corresponds to the SVG specification of SVG groups.

See Processing Documentation for adding child objects to PShape Group objects: 
https://processing.org/reference/PShape_addChild_.html

Below is an example of a function in the main tab that would create a PShape group and return that PShape group object so it can be used outside the function.

```java
//main tab code

void draw(){
// other code

agents = new Agent[numAgents];// initialize array
  for (int i=0; i<numAgents; i++){
    float x= random(0,width);
    float y= random(0,height);
    float size = random(50,100);
     g = createGroup(g, size);  ///call custom function below
     agents[i] = new PShapeAgent(x, y, size,g);
    }
 
 
 ///other code in draw()
  }
  
///Function in main tab to create a PShape group:

PShape createGroup(PShape g, float size){
    PShape p = createShape(RECT, 0,0,size,size);
    PShape p1 = createShape(RECT, 0,0,size/2,size/2);
  
    g = createShape(GROUP);
    g.addChild(p);
    g.addChild(p1);

    return g;
}


```

How can we use random variables to control how many children objects are displayed for each PShape group that is a PShapeAgent?
We must define an instance variable to keep track of how many children we show per object.

```java

class PShapeAgent extends Agent{
  PShape p;
  int num;  //variable to keep track of number of children to display  

//constructor using float for position: x, y
PShapeAgent(float _x,float _y, float _r, PShape _p){
   super(_x, _y, _r);
   p = _p;
   
   if(p.getChildCount() > 0){
     num = (int)random(1, p.getChildCount()); //randomly set number of children each agent  will display
   }
   else{
     num=0;
   }
   
  }//end constructor

//constructor using PVectors for position, speed
  PShapeAgent(PVector _position,PVector _speed, float _r, PShape _p){
   super(_position, _speed, _r);
   p = _p;
   
   if(p.getChildCount() > 0){
   num = (int)random(1, p.getChildCount()); //randomly set number of children each agent  will display
   }
   else{
   num=0;
   }
   
  }// end constructor
  
 void display(){
    translate(position.x, position.y);
    
     if(p.getChildCount() == 0){ // no children
      p.setFill(color(hue ,200,200,alpha));
      p.setStroke(color(50, alpha));
      shape(p, 0, 0 );
    } 
    else{  //has children
    PShape c;  //
    for(int i=0; i<= num; i++){
      c = p.getChild(i);
      c.setFill(color(hue + 10*i,200,200,alpha));
      c.setStroke(color(50, alpha));
      shape(c, 0, 0 );
     }
    } // end else
    resetMatrix();
    
  } // end display
  ```