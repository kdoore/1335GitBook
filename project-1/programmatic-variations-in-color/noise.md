# noise\( \)

Example using [Processing noise\( \)](https://processing.org/reference/noise_.html) function in comparison to using random\( \)

```java
//Noise example, input is a continuously increasing value - like framecount
//noise output is a value between 0.0-1.0, here we multiply it by height to give 
//a value for n that is between 0-height.
//Here, the origin is translated each frame to an x position with value of frameCount
//the y value for the red dot is set by the noise
//the y value for the blue dot is random

void draw() {
  frameRate( 10);
  noStroke();
  if ( frameCount < width) { //only execute while in window
    translate( frameCount, 0);
    float n = noise(frameCount * 0.1) * height;  //get a noisy y value
    fill( 255, 255, 0, 50);
    for ( int i=0; i< height; i+=5) {  //increment i by 5
      ellipse( 0, i, 5, 5); //draw a yellow ellipse at y value of i 
    } //end for
    fill( 255, 0, 0);
    ellipse( 0, n, 8, 8); //noisy y value - red dot
    fill(0, 200, 255);
    float randY = random( 5, height-5); //set y randomly within range of height
    ellipse( 0, randY, 4, 4); //blue dot - random y
  }
}

```

