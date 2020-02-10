# Project 1 Steps:

1. Conceptual Art to Express Emotion / Energy 
   
**Step 1: Determine Emotions to express:**

See [Models of Emotion: ](/modeling-emotions.md), [Concept Maps](https://en.wikipedia.org/wiki/Concept_map), [Mental Models](https://en.wikipedia.org/wiki/Mental_model)

**Create Personal Situation Concept Map**
Select a personal situation that has an associated range of positive and negative emotions.  Sketch a concept-map to brainstorm the concepts and emotions associated with your situation.

* Divide your concept-map sketch into 2 regions:  Negative, Positive
* Put 'Situation' as the center concept \( no need to provide specific details about situation \)
* Add associated concepts to negative or positive sides
* Add emotions to each side, position the emotions to indicate the strength of emotion - with the strongest emotions located at the outer edges of the regions, neutral emotions near the central dividing line 
* Result:  Select at least 5 emotions to represent in your artwork, list these along the bottom of your concept map. 

1. **Complete Project Planning Document**

   * Tables:
     * Define variables: 
       * colors ( minimum of 3 custom colors required )
       * Pshape length ranges \(minLen, maxLen\)
     * Main Emotions: ordered list of 5 emotions
     * Determine Design Attributes
       * map function parameters for values on both sides of the negative / positive regions: how do values change as mouseX changes?

2. **Use planning document as a guide to complete the logic** to determine input parameters the RecursivePattern functions, for each region, negative, positive.

   * Negative - region:  0 &lt; mouseX &lt; balancePoint
   * Positive - region: balancePoint &lt; mouseX &lt; width

* **RecursivePattern function parameters:  ** are determined in the draw\( \) function, depending region and mouseX value: 

```java
//recursivePattern functions with parameters
void recursivePattern1(float len, int count, color c1  )
void recursivePattern2(float len, int count , color c1 )
```

**These are the main customizations you will do for this project **

**float len **- determined by region and mouseX

- use map\( \) to determine len for each region

`float len = map( mouseX, 0, balancePoint, maxLen, minLen);  // negative region`

- you must determine logic for positive region

**color c1, color cMain** - determined by region and mouseX

  - use map\( \) to determine gradientFraction

`float gradientFraction = map( mouseX, 0, balancePoint, 0.0, 1.0); // negative region`
  * use colorLerp\( \), gradientFraction to determine color for current MouseX position

`color curNegColor = colorLerp( colorMax, colorMin, gradientFraction); // negative region`
  * you must determine logic for positive region

  * determine probability for random pop of color, this can be set for each region, or can vary within each region using map\( \) to set value of float randPopColor

  `float randPopColor = map( mouseX, 0, balancePoint, 0.3, 0.6); //negative region example`

**int count** - recursion termination variable   
    use map\( \) to vary this value as mouseX changes \(optional\), or it can be constant across both ranges

`float numRepeats = map( mouseX, 0, balancePoint, 8, 4); //negative region example`

**RecursivePattern Functions:** You will have 2 different ones

```
 **Modify Brightness within the RecursivePattern functions:**

 - you must modify brightness   
```

```java
     float brightFraction = map( len, lenMin, lenMax, 0.5, 1.0); //example
     float bright = brightness( c1 ) * brightFraction;
```

* you can add small variation in hue

  ```java
    float hue = hue( c1 ) + random( -5,5);  ///add or subtract small amount to get analogous colors
  ```

** Recursive Function Call**  
   - You **must modify count for each recursive call**, this can be done when setting the input parameters as below.  
   You will modify **len** for each recursive call because we are creating nested shapes, multiply by a fractional value.

```java 
      //Recursive call within Recursive Function - must modify count, len values;
     RecursivePattern( len * 0.8,  count-1, c1 ); //reduce values: len, count
```



