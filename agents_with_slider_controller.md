# Agents with Slider Controller

In order to add interest to our complex system designs, we can add sliders to give the user the ability to modify the hue, sat, alpha or other design parameters.  To do this, we'll use the basic [slider class](https://kdoore.gitbooks.io/cs1335/content/slider_controller.html#slider-base-class) and the [HueSlider class](https://kdoore.gitbooks.io/cs1335/content/slider_controller.html#hueslider-child-class) developed earlier in the course.


Once we've included the basic Slider code and the HueSlider code as a tabs in our project, then in the main tab we can create an instance of a HueSlider by declaring a HueSlider as a global object and then initializing it in the Setup( ) function.


```java
// main tab

Slider hueSlider;

void setup(){
  size(800,800);
  colorMode(HSB);
  hueSlider = new Slider(50, height - 60, 150, 30, 0, 255, "HUE");
  
  ////other code
  
  } //end of setup
```  


In the draw loop, we should include code to check if the slider value has changed, if the mouse has been pressed.


```java
void draw(){
  background(50);
  if(mousePressed){
      hueSlider.checkPressed(mouseX, mouseY);
  }
  
  ///more code
  
  
  }// end of draw
  
```

Within the draw( ) loop, we need to set both the highlightHue and basicHue for each agent.  Since the HueSlider only gives us 1 value, we can just modify that value slightly for the highlightHue, so that we can see a visual  distinction between agents that are intersecting compared to other agents.

We want to insure that all hue values fall within the range of meaningful values, so we'll use modulus to 'wrap' values that exceed 255, so, for example, a hueSlider value of 200 can be used to create a highlightHue value of: 255 + 100 = 355.  Since 355 is greater than 255, it would display as red unless we use modulus to wrap the value back into the valid range:

255 + 100 = 355, this displays as red    
355 % 255 = 100, this displays as green

We'll want to put the code for setting these hue values within the outer for-loop where we loop through all agents, to insure we set the value for each agent.

```java

///for-loop to examine each Agent object
for (int i=0; i<numAgents; i++){
     
    // hue gets set by basicHue and highlightHue
    agents[i].basicHue = hueSlider.sliderVal;
    agents[i].highlightHue = (hueSlider.sliderVal + (100)) % 255; 
 
```


Finally, we'll need to add code to our custom function so that when we create a new PShapeAgent due to a grow() or shrink() event, we first get the current basicHue and highlightHue values of the current agent, then use those to set the values for the newly created agent: 

```java
//given an PShapeAgent object, create a new object with the newly changed value of r,
//the only way to change size is to create a new PShape object using the updated value of r
Agent createNewPShapeAgent(Agent curAgent){
       float size = curAgent.r;  //get updated r
       float hue = curAgent.basicHue;
       float highlightHue = curAgent.highlightHue;
       float alpha = curAgent.alpha;  //get current alpha
       PVector position = curAgent.position;  //get current position
       PVector speed = curAgent.speed; //get current speed
       g = createGroup(g, size);
       PShapeAgent newAgent = new PShapeAgent(position, speed, size, g);
       newAgent.alpha = alpha;
       newAgent.basicHue = hue;
       newAgent.highlightHue=highlightHue;
  return newAgent; 
}



```