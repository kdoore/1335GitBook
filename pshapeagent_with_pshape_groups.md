# PShapeAgent With PShape Groups


PShape objects have the capability to have a group of PShape objects which comprise a group, this corresponds to the SVG specification of SVG groups.

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
     g = createGroup(g, size);  ///call custom function
     agents[i] = new PShapeAgent(x, y, size,g);
    }
 
 
 ///other code in draw()
  }
  
///Function to create a PShape group:
PShape createGroup(PShape g, float size){
    PShape p = createShape(RECT, 0,0,size,size);
    PShape p1 = createShape(RECT, 0,0,size/2,size/2);
  
    g = createShape(GROUP);
    g.addChild(p);
    g.addChild(p1);

    return g;
}




```
