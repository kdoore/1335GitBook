---
description: Iteration and Recursion for Repeat Patterns
---

# A3: Repeat Patterns

**Behavior:  Patterns:** Looping, Fractal  
**Function**: Self-Similar Replication  
**Structure:** Recursion

If Life is a Game, These are the Rules:  _Cherie Carter Scott_

> **Rule 3:** _**There are no mistakes, only Lessons**_
>
> _**Growth is a process of experimentation, a series of trials, errors, and occasional victories**.  The **failed experiment** are as much a part of the process as the experiments that work. Cherie Carter Scott_
>
> _**Compassion:**  An Individual is capable of both great **compassion** and great **indifference,** he has it within his means to nourish the former and outgrow the latter._   Norman Cousins
>
> **Rule 4: A lesson is repeated until Learned  
> Lessons will be repeated** to you in various forms until you have learned them. When you have learned them, you can then on on to the next lesson.   
>
> **Challenge:  Identify and release the patterns that you are repeating** 
>
> **Cultivate:  Awareness, Willingness, Patience, Acknowledge Causality**

## Assignment 3 Overview:

The tabs below show examples for creating a PShape that includes an inner contour.  There is a simple example of a code for a recursive function that creates a PShape pattern 

{% tabs %}
{% tab title="PShape w/Contour" %}
![](../.gitbook/assets/screen-shot-2021-03-17-at-3.44.47-pm.png)
{% endtab %}

{% tab title="PShape Contour Code" %}
```java
//Code for shape above - with contour
//create custom PShape usign vertex points
PShape fallShapeContour( float w, float h, color c1 ) {
  PShape s = createShape(); //initialize PShape
  s.beginShape();
  s.vertex( 0, .25*h);  //1
  s.vertex( w*.75, 0);  //2
  s.vertex( w* .10, h* .50); //3
  s.vertex( w* .25, h* .75); //4
  s.vertex( w* 0, h* .75); //5
  s.vertex( 0, .25*h);  //6
  s.beginContour();
  s.vertex( 0, .25*h);  //6
  s.vertex( w* .10, h* .45); //7
  s.vertex( w* .40, h* .20); //8
  s.vertex( w* .10, h* .30); //9
  s.endContour();
  s.endShape(CLOSE);
  s.setFill( c1);
  return s;
}
```
{% endtab %}

{% tab title="Recursive Function" %}
![Simple Recursive Pattern example](../.gitbook/assets/screen-shot-2021-03-21-at-1.38.06-pm.png)

#### Example of Recursive Function  

See [Gitbook Section](../project-1/recursion/) for Details on writing Recursive functions

```java
//Example code to create a simple recursive function

int maxCount = 5;
color c1 ;

void setup() {
  size( 600, 600); //use size(600,600,P2D) if possible
  colorMode( HSB, 360, 100, 100, 100);
  background(0);
  c1 = color ( 200, 100, 100);
}

//When mouse is pressed, draw pattern at mouse location
void draw() {
  if (mousePressed) {
    translate(mouseX, mouseY);
    PShape s = createShape1(100, 100, c1 );
    recursivePattern( s, maxCount, c1); //here level is initialized at 5 because we decrement it inside the recursive function
    resetMatrix();
  }
}

//Simple Recursive Function
//Parameter: PShape s - rendered on canvas
//Parameter: int count - specify the number of repeats: recursive calls
//Parameter: color - reduce brightness - with each recursion
//task is to set size, color, then render PShape on canvas
//Terminates when count is less than 0
//Required - global variable: maxCount - used to determine scaleFactor
void recursivePattern( PShape s, int count, color c1) {
  if (count <1 ) { //termination condition
    return; //stop function execution by returning from the function
  }
  float scaleFactor = map( count, maxCount, 1, 1.0, 0.5); 
  s.scale(scaleFactor, scaleFactor ); //- task - create PShape by calling the vertexShape function
  color curColor = color ( hue( c1), saturation( c1), brightness( c1) * 0.8, 50);
  s.setFill( curColor);
  shape( s, 0, 0); //draw the shape on the canvas at x=0,y=0.
  s.resetMatrix();
  recursivePattern( s,  count-1, curColor ); //recursive call - changed values for count, color
}


//Rounded rectangle
PShape createShape1( float w, float h, color c1 ) {
  PShape s = createShape( RECT, 0, 0, w, h, 10);
  s.setFill( c1);
  return s;
}

```
{% endtab %}
{% endtabs %}

## Assignment 3 Details:  Recursion

### Recursive Patterns

* **Hand Drawing:** Draw A **Fibonacci spiral** using grid paper, draw a minimum of 7 cubes.
  * **Gitbook:  Post photo** of your sketch on Gitbook
* **Hand Drawing:**  Draw a **simple branching pattern** inspired by recursion
  * **Gitbook:  Post photo** of your sketch on Gitbook
* **Hand Drawing:**  Create **2 new Vertex PShapes** \( you must now have 4 functions that create / return vertex shapes\)
  * **Draw PShapes** on **grid paper** to specify width, height, vertex points
    * **One PShape** must include a **contour:** \( see tab above\)
  * **Gitbook:  Post photo** of your sketch on Gitbook

### Recursive Functions:  Programming:  Processing Program

1. Write **2 Recursive Functions** that take a **PShape as an input parameter** and display **PShapes in a pattern**
2. Function Signature



### Recursion - Self-similar repetition, base-case, recursive step 

> In mathematics and computer science, a class of objects or methods exhibits **recursive behavior** when it can be defined by two properties:
>
> * A simple **base case** \(or cases\) — a terminating scenario that does not use recursion to produce an answer
> * A **recursive step** — a set of rules that reduces all successive cases toward the base case.   
> * A [function](https://en.wikipedia.org/wiki/Function_%28mathematics%29) may be **recursively** defined in terms of itself.  A familiar example is the [Fibonacci number](https://en.wikipedia.org/wiki/Fibonacci_number) sequence: **F\(n\) = F\(n − 1\) + F\(n − 2\).** For such a definition to be useful, it must be reducible to non-recursively defined values: in this case F\(0\) = 0 and F\(1\) = 1.  [Wikipedia](https://en.wikipedia.org/wiki/Recursion)

![Ouroboros: 1478 drawing by Theodoros Pelecanos: Wikimedia](../.gitbook/assets/128px-serpiente_alquimica.jpg)

### Iteration: Repetition of a block of statements

> **Iteration** is the repetition of a process in order to generate an outcome.  
>   
> **Iteration** in computing is the technique marking out of a block of statements within a [computer program](https://en.wikipedia.org/wiki/Computer_program) **for a defined number of repetitions.** That block of statements is said to be iterated; a computer scientist might also refer to that block of statements as an **"iteration"**.  
>   
> The primary difference is that **recursion can be employed as a solution without prior knowledge as to how many times the action will have to repeat,** while a successful **iteration requires that foreknowledge**[  
> ****Wikipedia](https://en.wikipedia.org/wiki/Iteration)

#### Youtube Videos about Recursion and Fibonacci Sequence

1.  [https://www.youtube.com/watch?v=JSyQx9zdQAM](https://www.youtube.com/watch?v=JSyQx9zdQAM)
2. [https://www.youtube.com/watch?v=SjSHVDfXHQ4](https://www.youtube.com/watch?v=SjSHVDfXHQ4)
3. [https://www.youtube.com/watch?v=7bod8x0LgJs](https://www.youtube.com/watch?v=7bod8x0LgJs)
4. [https://www.youtube.com/watch?v=IGJeGOw8TzQ](https://www.youtube.com/watch?v=IGJeGOw8TzQ) 

## Inspiration

### **Feelings are Always Conscious**

> **To manage life’s problems we use emotions as a compass. It is feeling that guides all learning from experience.** But biology provides one further drive to help us on our way:  Mark Solms

{% embed url="https://a.co/9bacOKA" caption="Mark Solms" %}

> In order to solve the hard problem of consciousness, science needs to discern the laws governing **the mental function of ‘feeling’.** This is not just a matter of words. I marshaled considerable evidence to show that **feeling is the foundational form of consciousness,** its prerequisite. I also explained both **physiologically and mechanistically the difference between felt and unfelt needs and showed that feelings have concrete consequences.**  **‘Consciousness is not merely a subjective perspective upon the “real” dynamics of self-organizing systems; it is a function with definite causal powers of its own’.**  _Mark Solms_

> Hunger feels bad, and it feels good to relieve it by eating; a distended bowel feels bad, and it feels good to relieve it by defecating; pain feels bad, and it feels good to withdraw from the source of it. These are **bodily affects but the same applies to emotional ones**. Separation distress feels bad and we respond to it by seeking reunion. Fear feels bad and we escape it by fleeing the danger \(and sometimes by fainting\). Suffocation alarm and hunger and sleepiness and fear all feel bad, but they feel bad in different ways. **Getting rid of them, by contrast, feels good, also in different ways.”**

**The Law of Affect:**  voluntary behavior is guided by affect - You decide what to do or not to do on the basis of the felt consequences of your actions.

**Affective States: Mental States:** Affective States are hedonically valanced:  Good or Bad....Feeling sensations possess intrinsic value:  Good, Bad.  Pleasure and Unpleasure tell you how you are doing in relation to your biological needs.

**Affect and Arousal** are aspects of human experience that are essential for  survival.  Affect and arousal aspects of subjective human feelings have properties of  valence, magnitude, category, that are associated with unmet human drives.  

**Affective Experience is primarily a felt phenomena**, Feelings guide our behavior in conditions of uncertainty. ****Humans have the unique ability as complex organisms to 'register our own states - subjective being.

**Arousal accommodates emotional responsively and intentionality:** affective arousal enables volition

**Thinking is Virtual Action:** The capacity to try things out in the imagination - imaginary form of experience

**When feelings become conscious, drives measure demands made upon the mind for work.  A feeling disappears from consciousness when the need it announces it has been met. Felt needs are prioritized over unfelt needs. Priorities are determined by the relative strengths of your needs in relation to the range of opportunities afforded by your current circumstances. When you become aware of a need, when it is felt, it governs your voluntary behavior.  Choices can be made only if they are grounded in a value system...**

**Feelings make creatures like us do something necessary - they are measures of demands for work - Drive as a measure of the demand made upon the mind for work in consequence of its connection with the body**. **Affects are the subjective manifestation of drives - they convey which biological things are going well or badly for us and they arouse us to do something about them** 

There are **three types of affect:** homeostatic \(interoceptive\) and sensory \(exteroceptive\) ones \(both of which are bodily\) and **emotional ones** \(which involve the body but cannot be described as ‘bodily’ in any simple sense\).”

Affect: Primary Emotions, Feelings:  _Mark Solms_

* Lust
* Seeking - exploratory foraging: state: curiosity - default emotion
* Rage - Fight
* Fear - Flight
* Panic / Grief
* Care
* Play

Secondary Emotions: guilt, envy, shame, jealousy arise from conflict situations - learnt constructs - hybrids of emotions and cognition

## Culture as Patterns - 

### Rececca Solnit: Recollections of My Nonexistence - The Ordinary Voiceless

{% embed url="https://www.vanityfair.com/style/2021/03/rebecca-solnit-on-the-ordinary-voiceless" %}



