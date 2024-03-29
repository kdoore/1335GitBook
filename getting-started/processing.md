# Processing

{% embed url="https://Processing.org" %}

### **Processing**: a language, a library, a development platform

* Created by Ben Fry, Casey Reas at MIT MediaLab under direction of John Maeda - 2001
* There are multiple different language versions of Processing.&#x20;
* **The Java version that we'll learn in this course is the 'original' version**
* Khan Academy uses an _unofficial_ javascript language version of Processing
* **P5.js:**  Official Javascript version of Processing - Includes functionality to create and modify html.  Ideal for using on web pages
* **Codepen.io - Online Code Editor - Useful for learning P5.js**

{% embed url="https://codepen.io/kdoore/professor/WNxeGVz" %}

### Overview: Processing Development Environment (PDE)

* [**Download Processing**](https://processing.org/download/)****
* **Install Processing**
* **Open the Processing Application** -&#x20;
  * opens by creating a new sketch
  * save the sketch with a meaningful name.
* ****[**Processing.org Documentation:**](https://processing.org/reference/) **** Reference, Examples, Tutorials
* **Installing Tools, Libraries, Modes, Examples**
  * **Extended Code Completion**
  * **Reference Tool**
  * **Examples: Learning Processing, others**

{% embed url="https://processing.org/reference/" %}

Paste the following code into the code editor: then push the play button

```
int xPos;
void setup() { 
  size(800, 400);
  xPos = 0;
} 

void draw() { 
  background(100,50,255);
  fill(100, 255, 255);//cyan
  rect( (xPos += 5)% width, 50, 50,50);
  textSize( 30);
  text("Example of using java processing", 100,200);
}
```

![Processing Development Environment: Executes to generate the sketch canvas](../.gitbook/assets/screen-shot-2021-01-22-at-2.56.13-pm.png)

![Install Tools:  Menu: Tools > Add Tool](../.gitbook/assets/screen-shot-2021-01-24-at-2.18.06-pm.png)
