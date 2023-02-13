# Entry 3
##### 2/12/23

Over the past few weeks I have still been learning my tool, p5js. I have learned and practiced many more things. My two main sources are still the [p5js reference page](https://p5js.org/reference/) and [The Coding Train's p5js playlist](https://www.youtube.com/playlist?list=PLglp04UYZK_PrN6xWo_nJ-8kzyXDyFUw).

Since the last entry, the first things I did were basic shapes and their syntax. I learned how to make shapes like quadrilaterals, triangles, and circles in p5js with all of their unique syntax. One thing I did that was useful when practicing with the shapes was practicing plotting basic points on the canvas with `point(x,y);`. The point function simply takes in an x and a y value to plot on the canvas. Most if not all of the syntax for the other shapes would ask for at least one x and one y value to determine the location of the shape. However when looking through The Coding Train's videos I found a fun thing to code using the points that I decided to try out.

The video itself was mainly about a function in p5js called `random(min,max)`. The random function reminded me of math.random(); but except of picking a float between 0 and 1 it takes in a minimum and a maximum value to pick from inbetween. After learning this new function I immediently used `random();` to generate a number between 0 and 400 and then saved it into a variable that I used for both the x and y value of the `point();`. However the dots were not random and would form a linear decreasing line. I then decided to watch further into the video I was watching I noticed two differenced inbetween his and my code. The first difference is that they actually used `width` and `height` as parameters to fit to any canvas size. The second difference was that `random();` was used twice to make a variable of x and y to plug into the point parameters. 

After a while I realized what was wrong with my inital code. Since I was only doing `random();` once and used it for both x and y, it would use the same numerical value in the point for both x and y. So if the function chose 10 the point would be `point(10,10)` instead of the x and y being different and more random; this would explain the reason the dots seemed to form into a line. When I corrected my code I was happy to see the code functioning as planned and even added a bit of color.
```js
function setup() {
  background(0);
  createCanvas(400, 400);
}

function draw() {
  var x= random(0,width);
  var y=random(0,height);
  point(x,y);
  strokeWeight(5);
  stroke(200,5,100)
}
```
![not found](../images/p5js-testing-screenshot-1-blog3.PNG)

The next thing I played around with was similar to `point();` but it was `vertex(x,y);` which took in the same parameters as `point();`. The difference was that the vertices could be used to form a shape by connecting them together. To make a shape with the vericles you would use `beginShape();` to start the shape and then `endShape();` to stop making that shape. The verticles set inbetween those two functions counts towards the shape. The difference between this method and just using the other shape functions is that there is a limited amount of verticles you can set with the other shapes, but with this method you can make an unlimited amount of verticles. This allows for unique shapes and complete freedom over what you are making. 

I decided to then practice with this and ended up with a seven. One thing I found interesting when making this though was how I went about coming up with the coordinates and how important it was to think about the canvas as a grid. I ended up using estimation and testing a lot to end up with the shape.
```js
function setup() {
  createCanvas(600, 400);
}

function draw() {
  background(255);
  beginShape();
  vertex(50,50);
  vertex(200,50);
  vertex(150,200);
  vertex(100,200);
  vertex(125,100);
  vertex(75,100);
  vertex(50,50);
  fill(150,100,200);
  noStroke();
  endShape();
}
```
![not found](../images/p5js-testing-screenshot-3-blog3.PNG)

The next function I learned about was `arc();` which takes in an x & y value, width & height, starting angle, and a stopping point. When I first wanted to learn this function I thought it was just going to be a curved line but was suprised when it was more like making a circle. The first 4 parameters were self explainitory however the last two parameters I did not understand. The 5th parameter took in a number as an angle and the 6th parameter came in the form of a value of PI. To better understand how it worked I had to look up a circle with all the PI values.

After looking at my results I recognized what it was but it had been a while since I learned it. The PI value controled how much of a complete circle there was, `TWO_PI` being a full circle. However it took me a bit of observation and tinkering with the starting angle to understand what it was. After I looked at the circle diagram again I came to the conclusion that the 5th parameter represented where the circle started drawing in terms of the basic circle diagram. A circle starts at the right with a starting angle of 0 and goes around clock-wise. So if the 5th parameter is 20, then the circle with start at an angle of 20 which would be a bit around the right bottom of the circle.

After I got a good understanding of all the parameters of `arc();` I decided to practice by making various circles with different parameters, primarily focusing on changing the x & y, and the PI values. I also used this as a chance to practice javascript objects since it was a while since I last used them.
```js
function setup() {
  createCanvas(600, 400);
}

function draw() {
  background(255);
  var pieVariations= {
    oneSixTeenth: QUARTER_PI/2,
    oneEight: QUARTER_PI,
    oneForth: HALF_PI,
    oneHalf: PI,
    fiveEighth: PI+QUARTER_PI,
    threeForth: PI+HALF_PI,
    sevenEighth: TWO_PI-QUARTER_PI,
    wholePie: TWO_PI
  };
  
  arc(50,50,50,50,0,pieVariations.oneSixTeenth);
  arc(50,150,50,50,0,pieVariations.oneEight);
  arc(50,250,50,50,0,pieVariations.oneForth);
  arc(50,350,50,50,0,pieVariations.oneHalf);
  arc(150,50,50,50,0,pieVariations.fiveEighth);
  arc(150,150,50,50,0,pieVariations.threeForth);
  arc(150,250,50,50,0,pieVariations.sevenEighth);
  arc(150,350,50,50,0,pieVariations.wholePie);
  
  fill(150,100,200);
  noStroke();
}
```
![not found](../images/p5js-testing-screenshot-4-blog3.PNG)

One of the latest things that I have done was inspired by The Coding Train's video about making a bouncing ball. I didn't learn any new functions or anything but I ended up using conditionals. When I went into p5js I didn't think I would be using many conditionals at all and thought I would just be coding basic shapes and nothing more but this definately changed my perspective after I finished.

The goal was to make the circle bounce back when it hit the side of canvas. Before watching the rest of the video I thought it would be simple, with the x increasing by a certain increment if x got greater than the width then increment using a negative to make it go backwards. But it wasn't as simple as that because it didn't work. After watching more of the video I found that in order to make it work I needed to make another value to represent the increments rather have one value representing both location & increments of movement. I named the new variable `xsped` which was speed with one e because speed apparently was already a function so I couldn't put "speed" in the name.

I set my `xsped` to 5 so that the circle would move to the right by 5. Then instead of changing x directly I wrote if x is greater than the width then change the speed to -5 and go backwards. This worked so I completed what I set out to do but I wanted to add onto it. I wanted to make it bounce off all sides of the canvas. Where  I left off the circle would go to the right, bounce off the right side, start going left, and then dissapear off the left side. To make the circle bounce off of both sides I added onto my if statement with an else if statment saying that if x became equal to zero, set the speed to +5 again to make it go right. 

When I did this it worked and so I went to work on making the circle also bounce off the top and bottom of the canvas. I ended up doing the same thing I did with x to y, I created `ysped` and set it to 5. Then I made an if statement saying if y became greater than the height then bounce back if the following else if statement. When I tried it out it almost worked as planned but something was wrong. The circle bounced off of most sides perfectly except the top. The circle would exceed the top and not bounce back immediently like it should have. Instead it went off the canvas and would take about 3-6 seconds to return.

I found the error after looking carefully at the code. I knew the x stuff was fine and it bounced off the bottom fine so I knew the error had to do with the statement controlling the top side. This was the faulty code:
```js
  else if(x==0){
    ysped=5
  }

```
The problem with this is that it is supposed to say `if(y==0)` but I wrote x instead. This would explain why the circle would eventually come down but with delay. The circle would go off the canvas and past y=0 until it eventually hit either x=0 or the width and since the code for the x sides was working it would bounce the circle back down again. After changing the small error the circle correctly bounced off all sides. It reminded me of the DVD bouncing logo so in courtesy of that I made the colors of the circle's stroke change color using `map();` to make it actively change.
```js
var x=0;
var y=0;
var xsped=5;
var ysped=5;
function setup() {
  createCanvas(600,300);
}

function draw() {
  background(0);
  r = map(x,0,width,0,255);
  g = map(x+y,0,height+width,0,255);
  b = map(y,0,height,0,255);

  stroke(r,g,b);
  strokeWeight(4);
  noFill();
  ellipse(x,y,50,50);
  if(x>width){
    xsped=-5
  }
  else if(x==0){
    xsped=5
  }
  x= x+xsped
  
  if(y>height){
    ysped=-5
  }
  else if(y==0){
    ysped=5
  }
  y= y+ysped
}

```
![not found](../images/p5js-testing-screenshot-2-blog3.PNG)

I am currently still in the 3rd(Brainstorming) and 4th(Planning) stages of the Engineering design process because I am currently preparing for the project by learning my tool, p5js. I would say I practiced many usefull skills such as logical reasoning because of the practice I did with conditionals and how I combined it with p5js. I also practiced learning and reading by reading the documentation for many of the shape functions and learning by coding them myself. I also practiced googling because of the stuff I had forgotten with PI. Finally I would say I practiced debugging because the stuff I coded contained a lot more code and values allowing room for errors that I had to catch.

I plan to next try learning 3D shapes such as boxes, planes, spheres, ect. I had already tried doing the box once with correct syntax but it didn't work. After skimming though the 3D stuff I figured that it will be the next thing I strive to learn because I think that there is a lot that comes along with the 3D shapes beyond just the functions for the shapes. I look forward to learning more about coding 3D objects onto the canvas.

[Previous](entry02.md) | [Next](entry04.md)

[Home](../README.md)
