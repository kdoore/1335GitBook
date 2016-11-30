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
  }
```  


In the draw loop, we should include code to check if the slider value has changed, if the mouse has been pressed.


```java
void draw(){
  background(50);
  if(mousePressed){
      hueSlider.checkPressed(mouseX, mouseY);
  }
  
```