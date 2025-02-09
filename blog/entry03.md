# Entry 3
##### 2/8/25

I am currently on stage 2 on Engineering Design Process, which is researching tool to use on my solution. We had set up some goals for winter break and it was to start making the actual game. Here is how our goals looks like:
```
Plan for winter break: 
* A simple tilemap added to the project 
* add a character that players will control for the whole game  
  * the character can run around places 
* towers (don't need to design how it looks like yet) 
  * Player will need to go to construction building to build new buildings 

Add collision so that players cannot walk through a tower 
Camera follows the player
```

Unfortunately not all of these goals are achieved because it took us longer than expected to setup the project to code because of how godot is meant for solo development so in order to code together, we would have to use github desktop and connect it to godot by dragging godot project files into github repository files so when we make changes, it will detect it and we will be able to push it to github. Afterwards we created our sprite with no design on it but a square and add `movement.gd` into the sprite so that it can move. 

Then we create a building with Sprite2D and CollisionShape2D but without the `movement.gd` so it doesn't move. With CollisionShape2D, it allows us to adjust the size at viewport so they collides onto each other rather than passing through.
![image](https://github.com/user-attachments/assets/309be55d-416b-42fb-913a-85bc539c63fe)
I can't move if I press the up key. 


Lastly, we make the camera always center the player's sprite so it follows when the player moves. We do that by adding a child node Camera 2D into CharacterBody2D and then on the viewport, put the sprite in the middle of Camera2D and then when you run it, the camera would follow the player when it moves. 
![image](https://github.com/user-attachments/assets/33aa305b-4a0c-4ce3-982e-aa08373cc129)
![image](https://github.com/user-attachments/assets/fe57e8f9-ed07-499d-bd1d-5f287cdea330)
We haven't draw out our buildings and character yet


Despite we want to have a map ready by this winter break, the process of doing so is very complicated and it takes a lot of time because we have to draw every tile first before we are able to make a tilemap. Drawing is not a skill that I am confident at therefore it would be very difficult to create a tilemap throughout this winter break. Therefore our goal is to continue creating the tilemap meanwhile I also want to try to learn to make buildings interactable so we can make buildings a little bit more useful rather than just there. 

Throughout this winter break, me and my partners have practicing communicating and collaborating each other. We have hop on discord voice calls together to set up our project so that everyone can work on our project and whenever my partners are stuck on something, I always try to help them by look into the problem and brainstorm solutions together. 





[Previous](entry02.md) | [Next](entry04.md)

[Home](../README.md)
