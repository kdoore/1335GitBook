# PImage GameObjects

In order to enhance our game, we'll use PImage or PShape objects to create our game objects.  The link below provides great resources for prototyping 2D games.

 
In order to have the Drops be PImage or PShape Drops, we need to create child classes of Drop.  These child classes should override the display( ) method.  How can you add bounding box variables: bw, bh, bx, by?
 
 ```
 class PImageDrop extends Drop{
  PImage p;
  PImageDrop(float _w, float _h, PImage _p){
    ///the default constructor of the base class
    p=_p;
    w=_w;
    h=_h;   
  }
  
  void display(){
   image(p,x,y,w,h);
    noFill();
    rect(x,y,w,h);
  }
} ///end of class PImageDrop
```
girl1.png

![](girl1.png)

star.png

![](star.png)

healthheart.png

![](healthheart.png)



Some Free - Public Domain 2-D Game Assets: 
 
 [Daniel Cook's Planet Cute](http://www.lostgarden.com/2007/05/dancs-miraculously-flexible-game.html)
 
 [Glitch Garden](http://www.glitchthegame.com/public-domain-game-art/)
 
 [Free Fantasy Maps](http://freefantasymaps.org/free-fantasy-maps/)
 
 [Open Game Art](http://opengameart.org/)
 
