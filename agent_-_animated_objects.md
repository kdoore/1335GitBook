# Agent - Animated Objects

We can build on Shiffman's intersecting Ball objects, by creating an Agent Class that inherits from the Abstract Pattern Class. The Pattern class gives us hue, sat, bright variables that we've used as design parameters that are controlled by custom sliders.

###PVector
We can use the processing PVector class to represent the idea that points in 2D space can be considered as 2D vector objects, with x, y components.  The PVector class provides a series of methods to operate on 2D or 3D vector objects.  We can use PVector to represent position and speed.  See the use of PVector below.


###Class Agent inherits from Pattern
```java

class Agent extends Pattern{
  PVector position, speed;
  float r;
  float  highlightHue, basicHue;
  
  Agent(float _x,float _y, float _r){
    position = new PVector(_x, _y );
    r = _r;  ///radius is for test intersection
    speed  = new PVector(random(1,3), random(1,3));
    highlightHue = 72;
    basicHue = 190;
    hue = basicHue;
  }
  Agent(PVector _position, PVector _speed, float _r){
    position = _position;
    r = _r;  ///radius is for test intersection
    speed  = _speed;
    highlightHue = 72;
    basicHue = 190;
    hue = basicHue;
  }
  
  PVector getCenter(){
   PVector center = new PVector();
   center.x = position.x ;
   center.y = position.y ;
   return center;
 }
  
  void highlight(){
    hue = highlightHue;
  }
  
  void reverseSpeed(){
    speed.x *= -1;
  }
  
  void display(){
    colorMode(HSB);
    fill(hue, 200,200,alpha);
    stroke(50, alpha);
    ellipse(position.x,position.y, 2*r,2*r); 
    hue= basicHue;
  }
  
   void move(){
    if( position.x >width || position.x < 0){
      speed.x *= -1;
    }
    if( position.y > height || position.y < 0){
      speed.y *= -1;
    }
    position.add(speed);
  }
  
  void grow(){
    if( r < 150){
         r++;
         alpha = alpha > 50? alpha -= 2: 50;  //ternary assignment operator
    }
  }
  
  void shrink(){
    if( r>10){
         r--;
         alpha = alpha< 200? alpha +=2: 200;
    }
  }
  
  boolean intersect( Agent a){
    boolean isIntersect = false;
    float d = PVector.dist(position,a.position);
    if(d < this.r + a.r){
      isIntersect= true;
    }
   return isIntersect;
  }
  
  
}


```


###Main Tab: 


```java

Agent[] agents; //declare array of Ball objects
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
    agents[i] = new Agent(x,y,size);
    
  }
  colorMode(HSB);
}


void draw(){
  background(50);
  
 ]
  for (int i=0; i<numAgents; i++){
    
     if( keyPressed && keyCode == UP){
      agents[i].grow();  //change r value
     
    }
    else if(keyPressed && keyCode == DOWN){
       agents[i].shrink();  //change r value
       
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

void mouseReleased() {
  loop();
}

```

