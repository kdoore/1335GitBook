 # PShapeAgent

Our goal now is to create a PShapeAgent class that inherits from the Agent class. In the last section, we develped code for the Agent class, we specified that Agent inherits from the abstract Pattern class. [Agent extends Pattern](https://kdoore.gitbooks.io/cs1335/content/agent_-_animated_objects.html)


Now, we want to extend our functionality to include PVector objects to specify position and speed of each Agent object.

PVectors can be used to represent a 2D or 3D value, where each PVector object has component values for x, y, (and z for 3D vectors). 

There are some difficulties that we'll encounter when trying to create a PShapeAgent class that behaves similarly to the Agent class, since PShape ojbects have their x, y position defined relative to the upper-left corner of the object, rather than the center x,y position of our ellipse shaped Agent object.  This impacts both the intersection testing, which now must check for intersection of rectilinear shaped objects.  


###PShapeAgent inherits from class Agent

```java
class PShapeAgent extends Agent{
  PShape p;
  
  PShapeAgent(float _x,float _y, float _r, PShape _p){
   super(_x, _y, _r);
   p = _p;
  }
  
  PShapeAgent(PVector _position,PVector _speed, float _r, PShape _p){
   super(_position, _speed, _r);
   p = _p;
  }
  
  void display(){
    p.setFill(color(hue,200,200,alpha));
    p.setStroke(color(50, alpha));
    translate(position.x, position.y);
    shape(p,0,0);
    hue= basicHue;  
    resetMatrix();
  }
 
 PVector getCenter(){
   PVector center = new PVector();
   center.x = position.x + r/2;
   center.y = position.y + r/2;
   return center;
 }
 
 
 boolean intersect( Agent a){
    boolean isIntersect = false;
    if(position.x + r > a.position.x &&  position.x < a.position.x +a.r  && position.y + r > a.position.y && position.y < a.position.y + a.r ){
      isIntersect= true;
    }
   return isIntersect;
  }

}

```

###Main Tab code - Create PShapeAgents 

With the PShapeAgent class, our goal is to be able to use a wide variety of PShape objects to create interesting patterns.   

```java
Agent[] agents; //declare array of Agent objects
int numAgents;
PShape p ;
int size;

void setup(){
  size(700,700);
  
  numAgents = 80;
  agents = new Agent[numAgents];// initialize array
  for (int i=0; i<numAgents; i++){
    float x= random(0,width);
    float y= random(0,height);
    float size = random(15,45);
    p = createShape(RECT, 0,0,size,size);
    agents[i] = new PShapeAgent(x,y,size,p);
    
  }
  colorMode(HSB);
}


void draw(){
  background(50);
  
  //for every agent, check all other agents to see if there's an intersection
  //if there's an intersection, change color of both agents and
  //reverse X direction of both agents using Agent class methods
  for (int i=0; i<numAgents; i++){
    if( keyPressed && keyCode == UP){
      agents[i].grow();  //change r value
      if (agents[i].getClass() == PShapeAgent.class){  //is this a PShapeAgent object at runtime?
         agents[i] = createNewPShapeAgent(agents[i]);  //in order to resize, we need to create a new PShapeAgent object
      }
    }
    else if(keyPressed && keyCode == DOWN){
       agents[i].shrink();  //change r value
       if (agents[i].getClass() == PShapeAgent.class){  //is this a PShapeAgent object at runtime?
        agents[i] = createNewPShapeAgent(agents[i]);
       }
    }
    else if(keyPressed && keyCode == RIGHT){
      noLoop();
    }
    
    for( int j = 0 ; j < numAgents; j++){
      if( i != j){
        if(agents[i].intersect( agents[j])){
               agents[i].highlight();
               agents[i].reverseSpeed();
               agents[j].highlight();
               agents[j].reverseSpeed();
               strokeWeight(5);
               //get center so we can draw line between intersecting object centers
               PVector centerI = agents[i].getCenter();
               PVector centerJ = agents[j].getCenter();
               stroke(#0C1501, 255);
               line( centerI.x, centerI.y , centerJ.x , centerJ.y  );
               strokeWeight(1);
        }
      }
     } ///end of inner for loop - j
     ///for all Ball objects - move and display the objects
    
   
    agents[i].move();
    agents[i].display();
    
    } ///end of outer for loop - i
  
   ///check for keypressed? 
}

//given an PShapeAgent object, create a new object with the newly changed value of r,
//the only way to change size is to create a new PShape object using the updated value of r
//then return the new object 

Agent createNewPShapeAgent(Agent curAgent){
       float size = curAgent.r;  //get updated r
       float alpha = curAgent.alpha;  //get current alpha
       PVector position = curAgent.position;  //get current position
       PVector speed = curAgent.speed; //get current speed
       p = createShape(RECT, 0,0,size,size);
       Agent newAgent = new PShapeAgent(position, speed, size, p);
       newAgent.alpha = alpha;
  return newAgent;
  
}

void mouseReleased() {
  loop();
}

```






