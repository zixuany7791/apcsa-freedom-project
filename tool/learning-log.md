# Tool Learning Log

## Tool: **Godot**
 
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

### 12/23/24

By watching [this tutorial](https://www.youtube.com/watch?v=fZ-CJIYPFMI), we have sucessfully created our project and have my partners to also be able to code in the project. Godot are mostly for solo developers therefore we have to use combine github and godot to be able to code with partners.
* Created a sprite where players will control throughout the game
* added movement script onto the sprite.

### 12/24/24

* Added camera lock so that when the sprite moves, the camera follows the sprite as well. (The sprite stays in the center of the screen always)
* Added a building by duplicating the sprite but removes the movement script. However this doesn't work well because they share the same scene so whenever I decided to change the size of the sprite, the building would change as well and so far we haven't figure it out how to make them have different scenes so we recreated the building so they don't share the same scene.

### 1/13/25
Followed [this tutorial](https://www.youtube.com/watch?v=_57alDBagSY) to learn how to interact with objects. 

* I find out the files are everywhere therefore I organized it a little bit by creating some folders
* Added Area2D node to both the building and the player, however currently it does nothing right now.
* Added a label that gives the message where when the player get close to the building, the label appears saying that you can press e to interact 

### 3/1/25

I have continued followed the tutorial to learn how to interact with objects. 
* Inside of Area2D of both player and building, I added a collisionShape2D so that when a player's interactable area touches another buildings interactable area. You can choose to interact with it.
* In order to do that, I added scripts in the Area2D
* When I run it, I realized nothing happens at all. While wondering why it doesn't, I checked the video's date and realized it is 2 years ago. So it was definitely outdated.
* So I switched to another [tutorial](https://www.youtube.com/watch?v=pQINWFKc9_k) that is more recent to see if it works. 
```GDScript
extends Node2D
@onready var interact_label: Label = $InteractLabel

# the array that stores the object that can be interact by the player
var current_interactions = [] 

var can_interact := true
 
func _input(event: InputEvent) -> void:
	if event.is_action_pressed("interact") and can_interact:
		if current_interactions:
			can_interact = false
			interact_label.hide()

func _process(_delta: float) -> void:
	if current_interactions and can_interact:
		# interact with the object that is closest to the player
		current_interactions.sort_custom(_sort_by_nearest)
		if current_interactions[0].is_interactable: 
			interact_label.text  = current_interactions[0].interact_name
			interact_label.show()
			
# See which interactable object is the nearest
func _sort_by_nearest(area1, area2):
	var area1_dist = global_position.distance_to(area1.global_position)
	var area2_dist = global_position.distance_to(area2.global_position)
	return area1_dist < area2_dist

# When the player enters an interactable area, the object gets added into the array
func _on_interaction_area_area_entered(area: Area2D) -> void:
	current_interactions.push_back(area)

# When the player leaves an interactable area, the object gets deleted into the array
func _on_interaction_area_area_exited(area: Area2D) -> void:
	current_interactions.erase(area)
```
By running this code, I have successfully interacted with a building despite nothing really happens because I haven't add any functionality to it yet. 

### 3/9/25

* Since Benjmain created the menu for construction building, I decided to add that menu to be part of my interaction so that when a player interact with something, the menu shows up.
* In order for the interaction script to have access to the popup menu, I would need to use preload(scene) to do it.
* After some copy pasting the popup menu script from benjamin onto interact script, I want to not have the player moving when the player is interacted with a building. In order to do that, I need to connect the movement script from the characterBody2D to interact script. Thankfully because the interact script is attached to the interaction component, which is a child node of characterBody2D. Therefore we can connect them by this line of code: `@onready var player = get_parent()`
* In the movement.gd, I created a `set_interacting_state` function that returns a boolean. Then I will use that boolean at the beginning of the _physics_process function and do if `set_interacting_state` is true, returns nothing so it would end the function and the player would not be able to move.
* Added esc key to stop interacting with a building, this allows players to move again.


### 3/23/25

Since we have testbuild.gd that creates a building whenever we left click, we tries to combine it with interaction_component.gd and buildingmenu.gd so that it can only create a building whenever the player interact with the building and choose what building they want to create.
* We tries by sending a signal when the player choose what building they want to construct so when the testbuild.gd receive the signal, it can construct the building. However this didn't work very effectively.
* By thinking this throughly, I realized that it is possible that we combine the testbuild.gd with buildingmenu.gd into one script so you don't need the signal, you can just build after the player place down the building.

Afterwards, in order for the player to have a better idea of where they want to place their building. I wanted to have them seeing the entire map so they can have a better idea of where they want to place the building. 
* Created another Camera2D node called MapCamera
* Make it zoomed out, but because our tilemap is square meanwhile the camera isn't so what we did is we zoomed out either way.
* add swap functions in the interaction_component.gd for when interact with the building, it switches to the map camera meanwhile switches back when the player exit out of the interaction.

### 3/31/25

This week, our plans look like this: 
* Make the building sprite move with the mouse (Benjamin)
* Buildings should not be able to stack (Me)

Because I likes to procrastinate to the last day, by the time I started working on the project, Benjamin already did the first one but there are some flaws that still needed to be fix. 

By looking over his code, and testing out the code. I have found out that after the player stop interacting with the building, the building that is suppose to follow the mouse doesn't disappear, when it pass by the player, rather than going through the player, it pushes the player instead. 

So in order for that to not happen, I need to export the `building_menu.gd` and imported in `interaction_component.gd` so I can use the function `cancel_building_placement()` in `interaction_component.gd` that when I press escape or exit interaction. The building will stop following the mouse. 

After fixing some flaws for Benjamin, I started what I should be doing today, fixing the overlap issue of the building. In order to that, I remember that P5JS has this dist function that measure the distance between two points. So I went on the godot documentation to see if there are this type of function. Thankfully, it exists and it is called `distance_to()` So all I need to do is add all the buildings location that are in the game into an array and use a for loop to measure the distance between the building that the player is trying to place down to all the building that is created in the game. If it is less than 45, then they cannot place the building there. 



<!-- 
* Links you used today (websites, videos, etc)
* Things you tried, progress you made, etc
* Challenges, a-ha moments, etc
* Questions you still have
* What you're going to try next
-->
