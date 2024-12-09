# Tool Learning Log

## Tool: **Unity**

## Project: **The New Settlement**

---
### 9/30/24
Things that I have learned today:
- GameObject = containers for components, usually represent characters, props and scenery. (Camera is also a GameObject)
- Component
	- Physic 2D 
		- Rigidbody 2D = add Gravity to the GameObject 
		- Circle Collider 2D = hitbox 
			- You can use offset to move the circle 
			

Things that I have done today:

-By following this video https://www.youtube.com/watch?v=XtQMytORBmM, I have set up unity on my computer. 
- Robbed the bird that he was using in the video as my sprite (we don't talk about copyrights :D) 
- I added Rigidbody 2D on a GameObject and I was expecting my bird to drop but instead it went up instead. But what really happened is that I added Rigidbody 2D on Camera so its the Camera falling instead of the bird falling which makes it looks like the bird went up. 
- Added Circle Collider 2D to the bird and adjust the circle with offset so it looks right. I also make the circle a little bit smaller since the video 

### 10/27/24:

Context: 
Because I heard people saying that GoDot is better than Unity in class. I decided to do some research and have some discussions with my group members. Below are some summary thoughts of what I have researched: 
* There are many people that prefers GoDot over Unity because GoDot is more friendly for game developers who seek to do it for fun. 
* There are people that said that Unity are more for big companies and GoDot is more for solo developers or small companies.

With a little bit of researches of people's opinion about these two game engine, we decided to try GoDot today to see if GoDot can be a better tool to create our game. 


I decided to follow this [Tutorial](https://www.youtube.com/watch?v=QPeycNt29tY&list=PLfcCiyd_V9GH8M9xd_QKlyU8jryGcy3Xa) and to see how the starting progress looks for GoDot. In result, I don't see much difference since GoDot also have a lot of pre-made modules already that allows you to do a lot of stuff already without writing a single lines of code. Also, you can't really just play around with unity or Godot without any tutorial or guides to show you how it looks like and how it suppose to work. 

### 11/11/24 Continue learning godot

I have continue followed the video from last week and this is what I did: 
1. First I add a CharacterBody2D node in Node2D, or scene.
2. Then I need to add Sprite2D as a child node to CharacterBody2D to add a sprite picture in it so it looks like something. 
3. Then I added CollisionShape2D as a child note to CharacterBodt2D to add a hitbox sort of thing to the sprite, I assign a shape and adjusted the size of the circle so that it matches the sprite size.
4. Once I was done, I click on CharacterBody2D and "save branches as scene". Then all the child node from CharacterBody2D disappeared but now when I want to move the sprite, the hitbox comes along with it as well.

The save branches as scene is very nice because it makes the scene a lot more cleaner and it is easier to organize as you can click into the GameObject for more nodes to show up. 


### 11/23/24 Creating first GDscript

I have continued followed the video and this is what I did: 

1. Created the first GDscript and use it to add movement to the sprite when we press certain keys.
2. Went to project setting -> input map and created inputs for it to detect when running.
3. The code that the video uses for movement seems to be outdated since the code is a bit different. So I pull up the godot documentation and use the code from there instead.
```
extends CharacterBody2D

@export var speed = 400

func get_input():
	var input_direction = Input.get_vector("left", "right", "up", "down")
	velocity = input_direction * speed

func _physics_process(delta):
	get_input()
	move_and_slide()
```

### 12/8/24

I have continued following the video and this is what I did: 

1. added AnimationPlayer in CharacterBody2D
2. because my sprite was not animated, I decided to rob the assest that the video is using.
3. In AnimationPlayer, I created an idle animation for Sprite2D when the character is facing each direction by switching image at a certain amount of time (switch every 0.2s for a total of 0.4s).
4. You can change how the animation runs with the button next to the total animation time. For example, you can make it run like a loop or make it run like pingpong where it goes to the right and left.
5. In AnimationPlayer, I created an walking animation for Sprite2D when the character is facing each direction (switching every 0.1s for a total of 0.3s)

It is very interesting how animation works because it kinda shows that make something to have movement is basically switching images every miliseconds or every frames. The shorter time it take to switch image, the smoother it will looks but it can also means faster. 







<!-- 
* Links you used today (websites, videos, etc)
* Things you tried, progress you made, etc
* Challenges, a-ha moments, etc
* Questions you still have
* What you're going to try next
-->
