#Paddle Object


In the previous section, we reviewed Daniel `Shiffman's` Rain Game, Object-Oriented Game.  Now, we want
to customize the game to make it a bit more interesting.   The next change we'll make is to add a
paddle that can catch or hit the falling objects.  If we allow the objects to bounce, then that could
provide a user with extra scoring opportunities.  For now, let's just look at how we can implement
a paddle that moves left and right in response to keyboard input.  


###KeyPressed Event

The processing reference code for the keyPressed function can help us determine how to move the paddle object in response to a user's keyboard interaction.  Below is the processing example code

```	
	// based on code from http://processing.org/reference/keyCode.html
	
	void keyPressed() {
  		if (key == CODED) {
  			if (keyCode == UP) {
      			paddleY = paddleY – 30;
    		} else if (keyCode == DOWN) {
      			paddleY = paddleY + 30;
      			}
      		}
      	}
      	
```

In the code above, the first thing is to note that we want to know if the user has interacted with
our program using the keyboard.  If that's happened, then a keyPressed event is triggered.
Similar to mousePressed events Processing provides a function keyPressed( ) that is triggered
when the user interacts with the keyboard. Then, within the keyPressed( ) function, we need 
to determine how we want our program to respond to the keyPressed event. The keyPressed event
stores the a key value, and it remembers the most recent key that has been pressed.  For special
keys like arrow keys, we need to also use the keyCode values, so we can tell if the key that was 
most recently pressed corresponds to a special key, the arrow keys.  In the code above, 
keyCode == UP, is used to determine whether to move the paddle upwards.  

For our project, we'll be using a paddle that moves horizontally, so we'll look at whether
keyCode == LEFT, or KeyCode == RIGHT, and then we'll need to create code that changes the
behavior of our paddle's movement based on these keyCode comparisons.

###KeyPressed Event Handlers

First we need to create a Paddle class:  This will be simliar to the Ball class, but we'll have a rectangular object that moves based on the users keyboard interactions.  So, instead of the move() method, we'll have  pressedLeft() and  pressedRight() methods::

```	
	//this code is part of the Paddle class definition
	
	void pressedLeft(){
       if(x>0){   //check to make sure that the paddle doesn't move off the left edge
          x=x-speed;  // decrease x position to move the paddle left
        }
      }
      void pressedRight(){
     	if(x+pWidth<width){  //make sure paddle stays within the right canvas border
       		x=x+speed;
     	}
     }
```

The other methods and constructors are basically just like the Ball object, where we have paddle position coordinates: x,y and paddle dimensions pWidth, pHeight.  We also have a speed variable that controls how fast the paddle moves.

###KeyPressed boolean
If we wanted to provide the user with the ability to continually move the paddle by holding the arrow keys
down, we'd want to use the `keyPressed` boolean variable to check within the draw loop for each frame of execution if one of the arrow keys is being pressed.  We can still use the Paddle class event handlers, however we need to move our keyPressed tests and execution of eventHandlers to the draw loop.  This could provide smoother game-play.

Can you write code to have the paddle move more responsively?  This code will go directly in the draw loop instead of in a separate function as above: 
```
if(keyPressed){
    if (key == CODED) {
  			if (keyCode == LEFT) {
      			// what goes here?
    		} else if (keyCode == RIGHT) {
      			//what goes here?
      		}
      }
}
```