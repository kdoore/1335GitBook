#Grid Pattern Designs

![](/assets/Screenshot 2017-09-12 12.10.55.png)

The image above shows a grid-based pattern that we'll create and use as a guide to create more complex design patterns.
We'll use [Victor Vasarely's](https://kdoore.gitbooks.io/cs1335/content/vasarely.html) artwork as inspiration for creating grid-based abstract art.

When we look at this image, we can see some design patterns - if we can decompose the design to a set of rules, then we can begin to understand how to write code to create it.

###Observing Patterns and Rules in the Design: 

- shapes are arranged in a grid of rows and columns
- colors are changing across the rows and columns
    - hue varies according to ROYGBIV pattern
    - part of each pattern has full Sat, Bright
    - part of each pattern has reduced Sat, Bright
    
- background color - grayscale changes across the rows and columns

- Number of rows, 10 == number of columns 10
- Cell width == cell height

###Variation

Below we can see a more interesting design than the one above, where we've introduced a slight variation on the design in each grid position.  One modular unit has a smaller opening, and the sat / bright values are much lower for these modular units. Then we select randomly between these 2 modular units for each position based on 2 slight variations of the design motif. We've also added some randomization to the background color.  The resulting design is more interesting than the one above.  We see clusters of brightness that draw our interest.  Darker, duller areas recede in the design.


![](/assets/Screenshot 2017-09-14 13.05.19.png)

###Parametric Variation

Parametric Design focuses on creating tools to allow designers to make incremental variations on a single design idea. So, rather than writing a program to create a single design, we can create a tool to let us make small changes to the basic design...by modifying the design parameters that we think will give us an iterative design process. 

###Digital Prototyping

![](/assets/Screenshot 2017-09-14 10.53.42.png)

The image below shows an art quilt I had created in 1995. The design uses similar concepts of variations in saturation and brightness across modular units.  The ability to create a digital rapid-prototype of the designs would have been extremely helpful during the design and fabrication process, as cutting-out and sewing each individual piece for each modular unit was a tedious process. 

![](/assets/6fe73513013035befd149054d160506c.jpg)

[Vasarely - 1969 ](http://ncartmuseum.org/art/detail/ion) 
Vasarely's op art piece was created in 1969, he would also have benefited from digital prototyping tools for his Op-Art designs. 
