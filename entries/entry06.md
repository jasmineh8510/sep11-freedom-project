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



[Previous](entry05.md) | [Next](entry07.md)

[Home](../README.md)
