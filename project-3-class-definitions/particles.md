##Class Particle, Particle System

####Class Particle
Code below modified from Shiffman's Nature of Code


```java
//From Shiffman, Nature of Code, Chapter 4
//Modified to use PShape and to modify color: HSB with particle age
class Particle {
//Particle has location, velocity, and acceleration, PShape, color, lifespan
  PVector location;
  PVector velocity;
  PVector acceleration;
  float lifetime, lifespanMax;
  PShape s;
  color c;
  
  //CONSTRUCTOR
  Particle(PVector l, PShape s, color c) { //create particle at location: l
    location = new PVector(); //initailize PVector
    location.set(l);  //set location with parameter l
    this.s=s ;
    this.c = c;
//For demonstration purposes we assign the Particle an initial velocity and constant acceleration.
    acceleration = new PVector(0,random(0.1, .05));
    velocity = new PVector(random(-.5,1),random(-2.5,0));
  
    lifespanMax = random( 50, 100);
    lifetime = lifespanMax;
  }
 
  void update() {
    velocity.add(acceleration);
    location.add(velocity);
    lifetime -=1;
  }
 
  void display() {
    //Use changing lifetime compared to lifespanMax - to change brightness and hue
    if( s.getChildCount()==0){ //change fill if PShape does not have children
      float fractionDecr = map( lifetime, lifespanMax/2, 0, 1.0 ,random( 0.6, .2));
      float fractionIncr = map( lifetime, lifespanMax, 0, 0.8 ,1.0);
      s.setFill( color(hue(c)*fractionIncr, saturation(c)*fractionIncr, brightness( c) * fractionDecr));
    }
    shape(s, location.x, location.y);
  }
  
  void run() {
    update();
    if( frameCount %2 == 0){ //don't display every frame, use modulus to give pause
        display();
    }
  }
  
 
  boolean isDead() {
//Is the particle still alive?
    if (lifetime < 0.0) {
      return true;
    } else {
      return false;
    }
  }
}
```

####Class Particle System



```java
import java.util.Iterator;

class ParticleSystem {
//One list, for anything that is a Particle or extends Particle
  
  ArrayList<Particle> particles;
  PVector origin;
 
  ParticleSystem(PVector location) {
    origin = new PVector();
    origin.set(location);
    particles = new ArrayList<Particle>();
  }
 
  void addParticle(PVector location, PShape s, color c) {
   
   Particle particle = new Particle( location, s, c);
   particles.add(particle);
    
  }
  
 
  void run() {
    Iterator<Particle> it = particles.iterator();
    while (it.hasNext()) {
//Polymorphism allows us to treat everything as a Particle, whether it is a Particle or a Confetti.
      Particle p = it.next();
      p.run();
      if (p.isDead()) {
        it.remove();
      }
    }
  }
}
```

####
Example Main-Tab Code:
