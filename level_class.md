# Level Class

We want to add a Level class that acts as a data structure to keep track of all data relevant to each game level. 

We can add a variety of instance variables to the Level class.  We'll create an array of Level objects and a reference variable: curLevel to keep track of the current level.  

Level instance variables:
  int id;
  int lives;
  PImage bkgImg;  
 
Level Class Constructor Header:  What will the rest of this class look like given that there are no methods in the class.
```
Level( int _id, int _lives,  PImage _bkgImg)
```

In the main tab, we'll create our array of Level objects

```
PImage bkgImg1 = loadImage("background_blue.png");

Level[] levels = new Level[2];
levels[0] = new Level( 0, 10 , bkgImg1);
levels[1] = new Level( 1, 5,  bkgImg2);

Level curLevel = levels[0];
```

To set the background image, we'll create an image the size of the canvas and we'll use that instead of the background color so this is the first line of code in the draw loop, using the ``curLevel.bkgImg``

```
 image(curLevel.bkgImg, 0,0, 400,400); 
``` 

We will change levels when all drops have either been caught (intersected) or have fallen below the bottom of the screen (finished).  In Shiffman's code, this is when:  ``levelCounter >= drops.length``

This code below goes in the main tab, in the draw loop function, after the drop[i] loop code has ended.

```java


    // put in reset() function  //game method?
    // If all the drops are done, that leve is over! 
    if (levelCounter >= drops.length) {  //When levelCounter = 50
      //println("levelCounter inside if " + levelCounter);
      // Go up a level
      int maxLevels=levels.length-1;  //  if max index=1, maxLevels=1
      //println("levels length-1 " + (levels.length-1));
      //println("maxLevels " + maxLevels);
      if(curLevel.id +1 <= maxLevels ){  //go up a level if we have not hit the max level yet
        int index = ++curLevel.id; // increment to the next level ID and assign to indes
        println( "index " + index); //what is the next index
        curLevel=levels[index];  //change to next level
        println("curLevel changed " + curLevel.id);
      }
```
Below are slight variations of the SpaceCute Background Image from  [Daniel Cook's Planet Cute](http://www.lostgarden.com/2007/05/dancs-miraculously-flexible-game.html).  We can use these to prototype our Level bkgImg, but in your project you'll need to use different images.


![](background_b1.png)

![](background_purple.png)

![](background_teal.png)