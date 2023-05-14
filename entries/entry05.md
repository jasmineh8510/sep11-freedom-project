# Entry 5
##### 4/23/23

Over the past few weeks I have finished creating my minimum viable product (MVP) for pinball. I used the [p5js reference page](https://p5js.org/reference/) and the [p5play reference page](https://p5play.org/learn/) to help learn how to build my MVP.

Where I left off last blog I ended up having to re-write what I had from scratch using p5play this time. However it was not as hard as I thought. In-fact it was easier than just trying to code with raw p5js. The way I create a new sprite is by saving it as a variable. I started first by just trying to code the ball and make it like last time where if I click then the ball will spawn in that area at the top. So unlike the other sprites later on which I created in setup, I created the ball sprite in the `mousePressed()` function. Then each sprite has attributes you can adjust by making the `spite.attrubute` equal to a value and the cool thing about this is that based on the type of information you give p5play will be able to identify the shape you are trying to draw. So I assigned the x value to `mouseX`, the y value to 0, and the diameter to 50. After I did this I had the ball done.
```js
 function mousePressed() {
    ball = new Sprite();
    ball.x=mouseX;
    ball.y=0;
    ball.d=50;
    ball.color= GRAY;
}
```

After I made the ball I did the hardest part, the flippers. I had a vague idea of what I wanted and somewhat knew what I had to do. The left flipper was assigned to 'q' and the right flipper was assigned to 'e'; If q is pressed then I would need to rotate the left flipper to a certain point, and vise-versa with the right flipper. I started by coding the flippers into existance and making the if statements in `keyPressed()` which was very easy. The problem now was that I didn't know how to rotate the sprites so I went looking. I was looking in p5play for a while until I found [p5play's rotation page](https://p5play.org/learn/sprite.html?page=7) which contained a suprising amount of different ways to rotate a sprite. However since this was the MVP decided to do the 'teleport' rotation since all it did was rotate from one position to another with no in-betweens.

To do this I did,
```js
function keyPressed(){
    if(key=='q'){
        flipperLeft.rotation=45;
    }
    else if(key=='e'){
        flipperRight.rotation=45;
    }
}
```
However this gave me a problem. They both rotated the same way which isnt what I needed because I need them to both pivot upwards towards eachother. However I quickly came up with the solution to make one of the values negative so that they will tilt at the same angle but in another direction. After I solved this I ran into another problem which was that the sprite would not go back to their original position after I tilted them once. I decided to go to the p5js reference page to see if there was a function that would maybe stop once a key was no longer being pressed. However I couldn't find anything but I decided the closest thing to that would be a function called `keyReleased()` which would be activated when a key was released.

I wrote nearly the same code I did in `keyReleased()` that I did in `keyPressed()` but instead reverted the rotation to 0 degrees. This worked and I thought I could move on but when I tested it I noticed something weird happening. The ball would bearly interact with the flipper and if the ball was resting on the slipper and I tilted the flipper then the ball would stay in it's postion and become stuck on the page. I didn't know for a while why this was. At first I figured maybe the the ball was to big or the flippers were too small so I changed their sizes but nothing came out of it. Then after lots of thinking I speculated that since the rotation was more like snapping to another position that there wasn't any force behind the flippers to influence the ball in any way. This would mean I did need to use a rotation with a smooth transition. 

After looking at all of the different options p5play had I decided to used what seemed the best for me which was `sprite.rotateTo()`. The value it takes are an x and y value which the sprite will face towards. I replaced what I had with with `.rotateTo()` instead but nothing showed meaning there was a larger error. After checking the console it told me that I could not used `.rotateTo()` unless the flipper collider had been set to `'kinematic'` which would allow the movement of the sprite to be changed. I had orignally set it to `'static'` because I thought the gravity would influence the flippers. However to my suprise after I made the change the flippers worked well and looked nice.

My new code for rotating was:
```js
function keyPressed(){
    if(key=='q'){
        flipperLeft.rotateTo(-45,7);
    }
    else if(key=='e'){
        flipperRight.rotateTo(45,7);
    }
}

function keyReleased(){
    if(key=='q'){
        flipperLeft.rotateTo(0,7);
    }
    else if(key=='e'){
        flipperRight.rotateTo(0,7);
    }
}
```
While my code worked I noticed that there were many lines to my code, many were just chaging the attributes to a sprite by identifying the sprite's attribute and giving it a value. However I tried changing my setup for the ball by assigning the basic ellipse information into `newSprite()` as if it was `ellipse()` to see if I could refactor and it worked out well. Just like before, p5play can recognize what you are trying to draw based on the infomation you give it, which is the cool thing about it. After doing this I refactored the flippers and ended up with at least 15 less lines of code and it was a lot easier to look at.

Even though the ball would now interact with the flippers I still felt like there could be more of an impact. The reason I changed the rotation in the first place was because there wasn't enough momentum behing the flippers so I figured out would could give the flippers the extra power they needed. I decided that I would give the flippers a different point of rotation like real pinball flippers. Thankfully on the same page I found the rotations on I found how to change the x offset of the 'center' aka the center of rotation. So I changed both to 60 with
```js
flipperLeft.offset.x = 60;
flipperRight.offset.x = 60;
```
which was in `function setup()`. However I ran into something strange when testing. The right flipper would lower itself when rotating and it also rotated wrong. That is when I remembered I had a similar issue with the flipper rotation itself. I then decided to do what I did back then and made the right flipper have an x offset of -60 and it was functional with a lot more power! This meant all I had to do was create the walls. The walls were very simple and it took a bit of fiddling the the values to get the walls in a good position. In fact, a problem I ran into was that I started with the left wall but it went offscreen and up. After drawing the other walls I realised that they were being drawed from the center which is why their coordinated combined with their dimensions made them go offscreen. After adjusting most of the walls into the correct postion I created a top wall and went back to the ball so that I could have the ball spawn under the top wall. After many hours of work I had finally made a MVP.

I would say I am in stage 5(Create) and stage 6(Test) of the engineering design process because I have created a MVP and having been testing frequently in order to make it more efficent and functional. I used a lot of skills to get to this point. I had to be very considerate about how each thing I coded would effect the project. I definately had to do a lot of trail and error during this part because there was a lot that didn't work. I would have to take what I observed and then debugg to find a better solution which I did with the help of reading more documentation about what I needed. Even though I was in the middle of this project I still was learning the whole way through by testing and using the materials at my disposal. Over the next few weeks I should be finishing up my project, refining it, adding more substance, and making it look polished.

[Previous](entry04.md) | [Next](entry06.md)

[Home](../README.md)
