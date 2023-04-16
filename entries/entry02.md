# Entry 2
##### 12/19/22

Over the past few weeks I have been learning my tool, p5js. I can say that I learnt many things during the past weeks. My sources for learning have been the [reference page on p5js](https://p5js.org/reference/) and [The Coding Train](https://www.youtube.com/playlist?list=PLglp04UYZK_PrN6xWo_nJ-8kzyXDyFUwi) on youtube who has a whole playlist of videos about p5js.

One of the first things I learned was about the `setup()` function and the `draw()` function. Set up was for setting up the canvas and everything else you initally want to appear on the canvas before anything is drawn on it. The canvas is where the output of the code is shown and when doing `createCanvas()` you can set the length and width of the canvas. Locations of the canvas are treated like x and y coordinates and usually the top left of the canvas is considered 0,0 (The origin point). This is important to know if you want to draw a certain shape in a certain position.

When watching The Coding Train I learned about p5js's reference library. This library contains all the different functions and how to use them. That is how I discovered `fill()` and `stroke()`. `fill()` will fill in a shape with the color stated in the () and `stroke()` controls the color of the outline of your shape. `strokeWeight()` will then control the thickness of the outline and if you want no outline you do `noStroke()`. Functions like this will effect all the things you draw after them until you use them again with different settings. The color system of p5js is mainly centered around rgb which I had already learned in a previous year. A shape that I learned from the library that I worked with the most was the ellipse. The format of the ellipse is `ellipse(x-position,y-position,width,height)`. 

One of the first things I made when learning p5js was drawing ellispses wherever the cursor was when I pressed the mouse. I started by creating the canvas and setting the background color to white. Then I set a variable to contain the color I wanted for the fill of the ellipse. Then a important component I used was `if(mouseIsPressed)`, which made whatever was inside the if statement to happen while the mouse was pressed. Then after setting the stroke and fill I got to the ellipse. I knew I wanted the make a shape where the position of the cursor was but I wasn't sure if there was a way. I decided to look through the reference library until I found `mouseX` and `mouseY`. `mouseX` takes the x position of wherever the cursor is on the canvas and `mouseY` takes the y position of wherever the cursor is on the canvas. So I put them into the x and y values of the ellipse and it worked. Wherever the cursor was, if I pressed down on the mouse it would draw an ellipse and I was able to create very cool looking patterns.
```js
function setup() {
  createCanvas(1000, 1000);
  background(255)
}

function draw() {
var aColor = color(200, 0,100);
  if (mouseIsPressed){
    stroke(0);
    fill(aColor);
    ellipse(mouseX,mouseY,50,50);
  }
}
```
![not found](../images/p5js-testing-screenshot-1.PNG)

The next major concept I focused on was `map()` which I learned from The Coding Train. The concept seemed a bit confusing at first and I only felt like I fully understood what it did when I used it. The gist of `map()` is to convert a value into a different value on the basis that the values represent different things. I tried to re-create what The Coding Train did on my own. My goal was to make it so when the x position of the ellipse went to either side, the value would shift smoothly from black to white. I started by setting up the canvas and making the ellipse with a y position of 200 to be in the middle of the canvas. Then I created a variable named dark and set the value to `map(mouseX,0,400,0,255)`. This means whatever the x position of the cursor is, give the equivalent on a 0-255 scale. The reason the 2nd and 3rd value are 0 and 400 is because the canvas was 400px X 400px so the lowest x can be is 0 and the heighest x can be is 400. Then the reason the 4th and 5th values are 0 and 255 is because that is the range that rgb uses for color.

My code had resulted in an ellipse being created and following the x-position of my cursor and when I went left it got darker, but when I went left it got lighter.
```js
function setup() {
  createCanvas(400, 400);
}

function draw() {
  dark = map(mouseX,0,400,0,255);
  background(dark);
  
  stroke("red");
  fill(color(50,0,200));
  ellipse(mouseX,200,20,20);
}
```
![not found](../images/p5js-testing-screenshot-2.PNG)

Right after I had done this I went to go see if I could do this but relative to `mouseY`. So in `map()` I changed `mouseX` to `mouseY` and in ellipse the y became `mouseY` and x became 200 to be aligned with the center. This worked perfectly and the ellipse followed the y-position of my cursor and when I went up it got darker, but when I went down it got lighter.
```js
function setup() {
  createCanvas(400, 400);
}

function draw() {
  dark = map(mouseY,0,400,0,255);
  background(dark);
  
  stroke("red");
  fill(color(50,0,200));
  ellipse(200,mouseY,20,20);
}
```
![not found](../images/p5js-testing-screenshot-3.PNG)

After I had done all of this I wondered if I could do this, but instead of making the background fade to white; What if I could make it fade to a different color, like red. So I took the code I had and tried to change it. At first I thought maybe I could adjust the background to originally be red but then override it with my `map()` value that would make it fade from red to black. However this didn't work. My problem was that with rgb putting in only one value instead of 3 will make it grayscale and not a color. So after getting a bit of help and recalling how the rgb system works I learned that the 0-255 range in `map()` wasn't strictly for rgb. In reality it was just a numerical scale of 0-255 that could technically be used for anything, just in this situation I made it to be suited for rgb use. So if I wanted it to fade to red instead of white, for my background I needed to set my dark variable as the red value for background and then adjust the green and blue values as I saw fit. This made the code function as I had intended. The ellipse followed the cursor's x-positon and the further left it went the darker it got, but the more right it got the more red the background became.
```js
function setup() {
  createCanvas(400, 400);
}

function draw() {
  dark = map(mouseX,0,400,0,255);
  background(dark,0,50);
  
  stroke(250,0,50);
  strokeWeight(5);
  fill(color(50,0,200));
  ellipse(mouseX,200,20,20);
}
```
![not found](../images/p5js-testing-screenshot-4.PNG)

One final thing I wanted to test out was combining the first test I did with the one I just did. My intent was to get rid of the outline of the ellipse and fill the ellipse with a color based on the x-positon, essentially uncovering what would look like a gradient  whenever I would press the mouse. Like the first test my ellipse's x and y positions became `mouseX` and `mouseY` and would be drawn if the mouse was pressed. I then made a variable called `changeTo` and set it as `map(mouseX,0,1000,0,255)`. The 1st, 4th and 5th values were the same as the prior test but the 2nd and 3rd values are different because the canvas size is now 1000px X 1000px so the smallest x value is 0 and the biggest x value is 1000px. Finally I decided on the gradient being from black to blue, so for `fill()` I set red and green to 0 while I set blue to `changeTo`. The code worked on my first try and I impressed myself, and to me this is the most intriguing thing I have made with p5js so far.
```js
function setup(){
  createCanvas(1000,1000);
  background(255);
}

function draw() {
var changeTo= map(mouseX,0,1000,0,255);
  if (mouseIsPressed){
    noStroke();
    fill(0,0,changeTo);
    ellipse(mouseX,mouseY,100,100);
  }
}
```
![not found](../images/p5js-testing-screenshot-5.PNG)

This is part 3(Brainstorm) and part 4(Plan) of the Engineering Design Process because I am preparing for this project by learning how to use p5js. Over the past few weeks I feel like I have learnt a lot, especially when it comes to skills. I learned how to debugg because whenever I ran into a problem; like when I didn't know how to make the background change from black to red; I backtracked to what I knew about rgb. I also practiced learning on my own and reading documentation in order to efficiently and fully understand my tool, like looking on the p5js reference page and testing some of the things I found on there. Finally the biggest skill I practiced was having a growth mindset. If something wouldn't work I would keep trying and looking for different ways to do it until I got it to work. Overall I would say I made a good amount of progress the past few weeks.

[Previous](entry01.md) | [Next](entry03.md)

[Home](../README.md)
