#Project 1 Steps:

1.  Conceptual Art to Express Emotions
Determine Emotions to express:

See [Models of Emotion: ](/modeling-emotions.md) 

Select a personal situation that has strong associated emotions.  Sketch a mind-map / concept-map to brainstorm the concepts and emotions associated with your situation.  
    - Divide your concept-map sketch into 2 regions:  Negative, Positive
    - Put 'Situation' as the center concept ( no need to provide specific details about situation )
    - Add associated concepts to negative or positive sides
    - Add emotions to each side, position the emotions to indicate the strength of emotion - with the strongest emotions located at the outer edges of the regions, neutral emotions near the central dividing line 
    - Result:  Select at least 5 emotions to represent in your artwork, list these along the bottom of your concept map. 
    
2. Complete Project Planning Document 
 - Tables:
    - Define variables: 
        - colors 
        - length range (lenMin, lenMax)
    - Main Emotions: ordered list of 5 emotions
    - Determine Design Attributes
        - map function parameters for values on both sides of the negative / positive regions: how do values change as mouseX changes?
        
3.  Use completed planning document as a guide to complete the logic to determine input parameters for each region, negative, positive.  
    - Negative - region:  0 < mouseX < balancePoint
    - Positive - region: balancePoint < mouseX < width

RecursivePattern function parameters:  
    len 
    colorMain, colorVarient
    


        