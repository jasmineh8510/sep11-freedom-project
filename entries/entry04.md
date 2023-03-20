# Entry 4
##### 3/19/23

Over the past few weeks I have actually started my MVP (minimum viable product) and since starting this part of the process many parts and aspects of what I’ve been working towards have changed and I have also learned even more about p5.js during this process.

Before I even could make a plan or timeline for my project I felt that something was off. I didn’t feel like what I wanted to make had a reasonable purpose and so while I could make it I found it hard to make a plan based on it. That is when I considered changing what I wanted to make entirely, something more fun and engaging. That is when I looked at examples of the stuff that other people have done with p5js. Through this I noticed a whole different side to p5js that was more interactive and decided that was the route I wanted to take. I then started thinking about a thing I could make, perhaps a game. I then thought up an idea that I thought would be fun to code and to play; pinball.

With my new idea I had dozens of ideas of how to make it and with this I went to go make my plan. I broke down the components of my project and how to build it. The 3 main visible components would need to be a ball, flippers, and walls. All of the components would need to have collisions, the ball would need to be under influence of gravity, and the flippers would need to go up and down with a press of keys. With all of those components I would have a MVP and after just a MVP I have many ideas for going beyond that. My ideas for going beyond the MVP are to make more shapes for the ball to bounce off of, add a score system, and make everything look nice.

I already have started coding and I would say I am about 1/3s of the way towards having a complete MVP. I coded the ball and got gravity to work on the ball using code samples I got online, of course I understood what the code meant before putting it together and changing things. The code used physics with velocity, acceleration, and mass values. I wanted to make the ball appear when a user clicks a certain section of the screen only relative to x position. So I had to set the ball’s x position to the mouse’s x position which took me a few attempts. One reason why it didn’t work at first was because I made a x position variable inside the draw function but since it only exists within the function it doesn’t work. I had to set the variable outside of the functions and then make a function inside the function draw saying when the mouse it clicked, set the x to mouseX. This ended up working.

```js
function mousePressed() {
  xVal= mouseX;
  yVal = 0;  
  velocity = 0; 
}
```
Then I attempted to make the flippers at first by hard coding the shape with many vertices which was difficult in itself but then I would have to make another one to the right of the page and opposite facing from the original. 

```js
beginShape();
  vertex(350,650); 
  vertex(325,675);
  vertex(325,700); 
  vertex(350,725); 
  vertex(475,710);
  vertex(550,695); 
  vertex(550,690); 
  vertex(475,675); 
  vertex(350,650);
  
fill(100,50,50);
endShape();
```

This already proved to be a lot of work but then for the MVP all I would technically need are two basic lines or rectangles for flippers instead of a more realistic one. This was an example of me getting caught in little details and it has taught me to be more broad with my ideas for now. However before even making the simpler flippers I ran into another problem which was that I hadn’t figured out how to make the flippers have collisions and hit the ball. Then I remembered that p5js has many libraries and I had remembered seeing something about collision. The first one I looked at wasn’t the type of physics collision I needed however the second one was p5.play and it had exactly the things I needed. However there is a chance I might have to rewrite a lot of what I have because p5.play has “sprites” interact with each other so I would need to get the ball, flippers, and even the walls to be sprites. So over the next few weeks I will be working on my project and using p5.play to do so.

I am currently on stage 4(Planning) and stage 5(Creating) of the Engineering design process because I have been planning on how to make my project and I have been starting to create it. A skill I have been using a lot due to planning has been problem decomposition. Another skill has been debugging and slowly working through my code to find solutions. I also have read to find out about new libraries I could use for my project.

[Previous](entry03.md) | [Next](entry05.md)

[Home](../README.md)
