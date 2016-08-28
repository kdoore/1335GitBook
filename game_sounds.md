# Game Sounds

If we add the Processing Sound Library then we can add sounds to our game.

We can find sounds at sites like FreeSound.org, once you register on the site you can download open-source sounds for free.  If you include sounds in your game, you need to provide attribution for the sound resources.

Here's a link to a simple boing.wav sound that was downloaded from FreeSound.org: 
[CuteAnimal_Jump1: By OnlyTheGhosts](https://utdallas.box.com/boingWav)

Within the game, you need to put this sound file into your data folder.

You need to include the following library import statement at the top of your main tab.

```
import processing.sound.*;
SoundFile soundfile;   //boing.wav

void setup() {
  size(400,400);
  soundfile = new SoundFile(this, "boing.wav");
  game = new Game(); 
} //end of setup

```

Then, in your game, when you want to play this sound, you include this code: 
```
soundfile.play();
```

We can play when there's a collision with an ImageDrop

```
boolean idrop = drops[i].getClass().equals(ImageDrop.class);
if(idrop){
     soundfile.play();
}

```