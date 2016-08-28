# Game Class

We can refactor Shiffman's game code to provide a cleaner, more modular structure that is easier to understand, troubleshoot, and to extend.

 

Game Class Constructor:

```
//gameStates:///these must go in the main tab as a global variable
//if you want to use them in a switch statement

  final int START=0;  
  final int ACTIVE=1;
  final int END = 2;
  
  
 class Game{ 
  int currentState;

  int score;
  int lives;
  int numberDropsDone;
  int totalDrops;

  MenuArray menuButtons;
  Timer timer;        // One timer object
  Drop[] drops; 
  Level[] levels;
  Level curLevel;
  Paddle paddle;
  
  Game(){
    currentState = START;
    lives = 20;

    drops = new Drop[50];
    timer = new Timer(300);
    paddle = new Paddle(width / 2, height -170, 100, 171, 100/1.5, 171/2.0, loadImage("girl1.png"));

    Button[] btns = new Button[2];  //
    btns[0] = new TextButton(width - 50, 10, 40, 40, "Start");
    btns[1] = new TextButton(width - 50, 60, 40, 40, "End");
    menuButtons = new MenuArray(btns, 2);

    levels = new Level[3];
    initializeLevels();
    curLevel = levels[0];
  }
    

```
Game Class Methods: 
```
 void initializeLevels(){
      PImage bkg1 = loadImage("background_b1.png");
      PImage bkg2 = loadImage("background_teal.png");
      levels = new Level[2];
      levels[0]= new Level(0,30,color(#5F6795),bkg1);
      levels[1]= new Level(1,10,color(#5F9594),bkg2);
      curLevel=levels[0];
    }
    
    //use to reset values for new level
    void resetLevel(){
      numberLivesLeft = curLevel.lives;
      numberDropsDone = 0;
      timer.setTime(constrain((300-curLevel.id*25),0,300));
      totalDrops = 0; 
    }
    
    //use to reset entire game
    void resetGame(){
      curLevel=levels[0];
      score=0;
      resetLevel();
      startBtn.on=false;
      stopBtn.on=false;
    }
    
    void drawBackground(){
    
    }
    
    void play(){
    
    }
    
    void displayScore(){
    
    }
    
    void displayLevel(){
    
    }
    
    void displayGameOver(){
    
    }
    
    void drawBar(){
    
    }
    
    void drawButtons(){
    
    }
    
    void buttonClick(){
    
    }

    
 ``` 

Game play() method

```
void play(){
               if(keyPressed){
                if (key == CODED) {
                    paddle.PaddleKeyPressed();
                   }  
                } //end of if keypressed
            paddle.display();
     
            if (timer.isFinished()) {
              // Deal with raindrops
              // Initialize one drop
              float rand=random(0,1);
              if (totalDrops < drops.length) {
                 if(rand > 0.5){
                    drops[totalDrops] = new ImageDrop(starImage, 97,97);
                 }else{
                    drops[totalDrops] = new Drop();
                 }
                // Increment totalDrops
                totalDrops++;
              }
              timer.start();
            }
            ////Start of drops loop
            // Move and display all drops
            for (int i = 0; i < totalDrops; i++ ) {
              if (!drops[i].finished) {
                drops[i].move();
                drops[i].display();////// 
                if (drops[i].reachedBottom()) {
                  numberDropsDone++;
                  drops[i].finished(); 
                  // If the drop reaches the bottom a live is lost
                  numberLivesLeft--;
                  // If lives reach 0 the game is over
                  if (numberLivesLeft <= 0) {
                    gameOver = true; 
                  }
                } 
              // Everytime you catch a drop, the score goes up
                if (paddle.intersect(drops[i])) {
                  drops[i].finished();
                  numberDropsDone++;
                  score++;
                }
              }
            }////end of the drop[i] loop
        
            // If all the drops are done, that leve is over!
            if (numberDropsDone >= drops.length) {
              // Go up a level
              int maxLevels=levels.length-1;  //  if max index=1, maxLevels=1
          
              if(curLevel.id +1 <= maxLevels ){  //go up a level
                int index = ++curLevel.id;
                curLevel=levels[index];
                println("curLevel changed" + curLevel.id);
              }
             
             resetLevel();
            }
    }//end game.play()
    

```
  
MainTab Code:
```
Game game;

void setup() {
  size(400,400);
  game = new Game();
}

void draw() {
  game.drawBackground();
  
  if (game.gameOver) {
    game.displayGameOver();
  } 
  else {
     game.play();
     game.displayScore();
     game.displayLevel();
    }  //end of else
  
  game.drawBar();
  game.drawButtons();
  }  //end of Draw loop

  void mouseClicked(){
    game.buttonClick(mouseX, mouseY);
  }
 
```
