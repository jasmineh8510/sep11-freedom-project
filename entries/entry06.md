# Entry 6
##### 6/3/23
Over the past weeks I have gone from having my minimum viable product(MVP) to having my finished product along with having two presentations. In this blog I will go over how I completed my project and then go over my presentations.

## Beyond MVP and Completion
The first thing I did after making the MVP was making the ball only able to spawn ONCE if the user clicked within the game area. I originally wanted to use the `constrain()` function but when that didn't work I ended up just doing `if(mouseX>130 && mouseX<620)` as my conditon and that worked just as well. Then I ran into a problem, I didn't have any clue how to make the ball spawn only once. Then I figured out I could create a simple boolean value named `active`. This value would go on to serve as an on and off switch for my game to determine weither the game was active or not. I didn't know at the time but this value would come in handy for later. My code for spawning the ball was,
```js
 function mousePressed() { //Allows user to spawn 1 ball
    if(active==false){
        if(mouseX>130 && mouseX<620){ //Only will spawn the ball if user clicks within pinball area
            ball = new Sprite(mouseX,65,30);
            ball.color= 'lime';
            active=true; //The game is now active
        }
    }
 }
```
If the game was not already active and if the user clicks within the game area then the ball will spawn and the game will become active.

After I did this I made the flippers tilted downwards by default because before the ball would get stuck in the corners and there wasn't a risk of the ball falling. Due to this the game became a lot more practical. After I updated the ball spawning and the flippers I made some basic changes to the design. I decided I wanted a retro look so I made the background of the canvas and whole page black. Then to contrast this I made everything else a bright green. With these small changes my project started to look more appealing.

After this my next step was to add obstacles for the ball to bounce off. I did a sketch of the whole design before coding it. I made a design that was simple yet effective. I decided to use mostly triangles because with triangles at least 2/3 sides will not be perfectly vertical or horizontal which will allow the ball to roll off the obstacles without getting stuck on a flat surface. Up until this point I had only coded rectangles and circles so I thought that when I put in the inputs the `newSprite()` that the triangle would be auto recognized as a triangle. However this wasn't the case and I was confused at first until I read the error message. The function didn't know what I was trying to draw so I went to check p5play documentation and found that a traingle and other "complex polygons" needed inputs of arrays containing x and y values. After I found out what to do it was easy but tedious because I had to put in many values for all the shapes. There was also a lot of trial and error to see if the placement worked or needed to be changed. I had to change the values little by little until I found something that worked.

After I finished making the obstacles I wanted to work towards making a whole point system. The first step towards this was making obstacles that were worth points. I decided to make the obstacles themselves circles with a number inside indicating the amount of points they were worth. I made 4 point circles, one worth 10 points, one worth 20 points, one worth 30 points, and one worth 50 points. The one worth 10 is the easiest to hit and is closest to the flippers. The ones that give 20 and 30 are equal in difficulty to get and can be hit by getting the ball to go to the left or right of the 10 point circle. Finally the 50 point circle is the hardest to get and is sorrounded by obstacles. The only way to get the 50 is by timing the way you hit the ball so that either the ball hits the corner obstacles and bounces to hit the 50, or the ball hits near the top of the 20 or 30 and bounces to hit the 50. Through trial and error I managed to get the perfect placement for these circles and was ready to move onto making a point counter.

I started the point counter by setting `points` to 0 and then I made a function called `pointCheck()` which would check the collisions between the circles and the ball in order to add points. Inside the function there was if statements checking for if the ball collies with the circles.
```js
 if (ball.collides(fiftyPoint)){
    points+=50;
    console.log(points);
 }
```
After making the function I put it in the `draw()` function and thought it would work but it didn't. It bugged the whole game and the only error I got was "could not read properties of collides()". After this I re-typed my code, tried a different format, tried a different collide function, but nothing I did worked. After being stuck on this for a while I re-evaluated the way my code was running. That is when I realized that my error wasn't the code itself but the order at which things ran. Since `pointCheck()` was in `draw()` which ran constantly, the collision checking was checking all the time. However in the if statment it was checking the ball with the circles. The problem with this is that the ball only exists when the mouse is clicked but since that isn't immedient it wasn't reconizing the ball sprite. In order to fix this I had to use the boolean value from before. If the ball is spawned the game has started, so if the ball already exists THEN I should check for points.
```js
 if(active){
    pointCheck();
 }
```
After I made this change the point system started working and I checked the points via the console.

After I got the point system working I updated the instructrions and added the score display and updated `pointCheck()` so that when a collision happened the total points would be displayed. This worked on the first try and then I moved on to the last thing I wanted to do. Up until this point if the ball was lost then nothing would happen and to replay you would need to refresh. I felt like this would be very annoying to anyone trying to play my project so I decided to make it so there could be another ball spawned if there was a game over. I started this by creating the game over message first using the DOM in a new function called `lose()`. In this function if the ball's y value exceeded the height of the canvas then you get the game over message and `active` gets set to false. I put this function in `draw()` right where `pointCheck()` was. There could now be another ball spawned so at this point the only thing left to do was to reset the score and remove the game over message. 
```js
 if(active==false){
     if(mouseX>130 && mouseX<620){ //Only will spawn the ball if user clicks within pinball area
         ball = new Sprite(mouseX,65,30);
         ball.color= 'lime';
         score.innerHTML= "Score: 0"; //Score starts at 0
         points=0; //Resets the score after 1st time playing
         gameOver.remove(); //Removes the game over message after starting again
         active=true; //The game has started
      }
 }
```
After I did these things I had a game that functions correctly and was convenient to use.

## Presentations
When I made my in-class presentation my project was not fully finished. It still lacked the ability to be replayed without refreshing and only displayed score with the console. Even so I improvised made the slides based around my experiences up until that point. Using what I was taught a year pior about making presentations I really wanted to focus on making my slides intuitive. I wanted to do most of the explaining myself and largely used visuals to complement what I was saying. With a loose outline of what I wanted to say and the slides I practiced a few times and timed myself for 10 minutes. After this I was confident going in. During my presentation I suprised myself by speaking clearly without stuttering or swaying side to side. I am proud of how my presentation went. The slides can be viewed [here]( https://docs.google.com/presentation/d/1xI5ANK4RyT7WUZEPuaj0tSug6k73yFLYD4fbivIdV9Q/edit?usp=sharing).

For my elevator pitch I needed to condense my information as much as I could so I made a list of 10 things I needed to mention and then ranked them on importance. After this a developed a paragraph that quickly explained the game and the tools I used to create the game. I made the pitch in my [notes](https://docs.google.com/document/d/1u5wuiq-KeR1JvWJIWsnVYko7tOKR5m4c2ASgU0Kdo3k/edit#heading=h.fp9opay2w7zw) and then practiced alone and with classmates. Since I did this last year I definately felt more confident about my pitch. During the actual expo I was nervous that I would either mess up or that people wouldn't be interested but I was very wrong. Many people visited my project and it was a shock but it was encouraging. It also gave me many chances to give my pitch before having to present to the judges. When the time came I think I did good and I was told that my project was unique. Although I was tired of speaking by the end I am happy about how my pitch and presentations went. My favorite part was seeing people compete to see who could get the highest score.

## Conclusion
In this blog I demonstated being in stages 6(Testing), 7(Improving), and 8(Communicating Results) of the engineering design process. There was many skills I used and improved during the past few weeks. I was able to check various documentation to debugg my code. When I couldn't find an answer after looking online I was able to self-advocate and ask the others around me. I also had to be considerate of all aspects of my game in order to make it easily playable. Finally for the presenting of my project I had to manage my time and communicate my project to others. I prioritized what was most important to complete before the presentations and I had to figure out creative ways to present the game.

This project has been a very wild journey for me. At first I wasn't even sure what I wanted to make but through learning more it all came together to make this project. I learned a lot while making this project. I improved in my skills by a landslide and I am not only proud of the game but also myself for coming so far. I think I want to continue down the path of making games in the future. I want to go on from making simple games to more advanced ones and hopefully I will learn even more from making those.

[Previous](entry05.md)

[Home](../README.md)
