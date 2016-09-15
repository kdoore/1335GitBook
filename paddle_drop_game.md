# Paddle Drop Game


Based on Shiffman's RainDropGame, and on the program code for Learning Processing: exercise 10.4, we want to build a slightly more complicated game based on this program. Our game will use a paddle object to try and catch the falling drops. We’ll also use Object Inheritance to have several different objects that fall during our game, and we’ll use the PShape object to allow the use of .svg images for interesting drop objects. Also, we’ll use a Game class for methods and variables related to the game state, this will include Button class to start the game and to allow the game to be reset. A more advanced version of the game could also include gameLevels and other more advanced features

Planning
--------

To begin design of our game, let’s look at the changes we’ll need to make, to modify Shiffman's exercise 10.4 project code. In Shiffman's project, he has all of the game type code simply implemented within the processing draw loop. We’d like to re-factor his program and make a separate Game class in order to make it easier to organize and understand our program code. If we look at his Draw loop code, we can see that he’s incrementing a score-type variable, he’s keeping track of misses, etc. So, let’s create a Game Class, initially we can begin with the following instance variables, we will probably expand on these at some point:

### Game: Instance Variables

-   score: `int`
-   gameState: `int`
-   curLevel: `Level'
-   startBtn: `Button`
-   resetBtn: `Button`

We can use integer values to indicate the possible gameState values, this will allow us to use a switch(gameState) structure. We can use the keyword `final` to make it clear that these are values that shouldn’t be changed within the program :
```
    final int START=0;
    final int ACTIVE=1;
    final int END=2; 
    
    final int MAX_NUMBER_DROPS = 50;
    ```

Next, we’ll want a few methods, we may add more methods later, but we can immediately imagine we’ll need the following methods:

### Game: Methods
```
   display( ) : `void`
   reset( ) : `void`
   isGameOver( ) : `boolean`
```

 
