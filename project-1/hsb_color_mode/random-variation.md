---
description: Processing random( ) function
---

# Random Variation

Using random values can add visual interest to artwork.  The Processing `random( )`  function can be used in a variety of ways to create different types of variation.

**`//returns a float value between min, max, does not include the max value  
float random( float min, float max )  
float random( float max ) // 0 assumed to be the minimum value`**

### Random Probability of Event Likelihoods

The Processing random function can be used to determine random probability of an event occurring, where the event is displaying some differential content each time an event happens.  The event can be the frame-loop in draw, or it can be a user input such as mousePressed, or some combination events.  

**Event Likelihoods:**   In the following example, the random function returns a float value in the range between 0.0, 1.0.  Using if / else conditional logic based on the value of the random value generated, the code below will print "option1" approximately 50% of the time.

**`//example  
float randChance = random( 0.0, 1.0);   //will return values between 0.0, .9999  
if( randChance < 0.5) { //select midpoint of random range   
println( "option1"); //printed ~50% of the time  
}else{  
println( "option2"); //printed ~50% of the time  
}`**

### Random Variation: Color variation

Although random can be used to select all components of a color, such as when using colorMode\(RGB\): example:  
 **`fill( random( 255,), random( 255), random(255)); //random color`**

It's useful to use random\( \) to generate a small variation in a HSB color by decomposing a given color into it's hue, saturation, brightness, and alpha components and then using random\( \) to create slight variation in each color component value:  
example:  color variation if the following code is executed in the draw loop  
  
**`color c1 = color( 270, 100, 100, 100); //HSBA  
float hueVariant = hue( c1 ) + random( -10, 10); // 20 degrees of variation  
float satVariant = saturation( c1 ) - random( 0, 30 ); // subtraction gives 30 percent variation in saturation  
  
fill( hueVariant, satVariant, bright( c1 ) , alpha( c1) );//color variation  
rect( mouseX, mouseY, 100, 100); // drawn at mouse position`**

