---
description: Processing random( ) function
---

# Random Variation

Using random values can add visual interest to artwork.  The Processing `random( )`  function can be used in a variety of ways to create different types of variation.

**`//returns a float value between min, max, does not include the max value  
float random( float min, float max )  
float random( float max ) // 0 assumed to be the minimum value`**

### Random Probability

The Processing random function can be used to determine random probability of an event occurring, where the event is displaying some differential content each time an event happens.  

Event Likelihoods:   In the following example, the random function returns a float value in the range between 0.0, 1.0.  Using if / else conditional logic based on the value of the random value generated, the code below will print "option1" approximately 50% of the time.

**`//example  
float randChance = random( 0.0, 1.0);   //will return values between 0.0, .9999  
if( randChance < 0.5) { //select midpoint of random range   
println( "option1"); //printed ~50% of the time  
}else{  
println( "option2"); //printed ~50% of the time  
}`**

### Random Variation



