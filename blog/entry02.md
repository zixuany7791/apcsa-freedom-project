# Entry 2
##### 12/15/24

I am currently on stage 2 on Engineering Design Process, which is researching tool, I continued watching [Michael Game Tutorial](https://www.youtube.com/playlist?list=PLfcCiyd_V9GH8M9xd_QKlyU8jryGcy3Xa) and so far I have learned how I can play around with godot settings such as viewport, sprites graphic, and adding user input into input mapping so godot will observe this inputs. I also learned how I can create a GDScript to code a sprite's movement and add animation when the sprites are moving. 

However, as I am following this video, there is this one problem that I have faced. In the video, he used this to connects users input to the sprites movement.
```
class_name Player extends CharacterBody2D


var move_speed : float = 100.0
# Called when the node enters the scene tree for the first time.
func _ready():
	pass # Replace with function body.


# Called every frame. 'delta' is the elapsed time since the previous frame.
func _process(delta):
	var direction : Vector2 = Vector2.ZERO
	direction.x = Input.get_action_strength("right") - Input.get_action_strength("left")
	direction.y = Input.get_action_strength("down") - Input.get_action_strength("up")

	velocity = direction + move_speed
	pass
```
When I am trying to run this code, it says that there is an error at line 16 saying that invalid operands Vector2 and float for + operator. I end up going to gdscript documentation to see what is Vector2 but what I found instead is that it seems like this code is outdated which turns out that it doesn't work anymore. So I found this code instead for connecting user input to sprites movement. 
```
class_name Player extends CharacterBody2D


var moveSpeed : float = 100.0
# Called when the node enters the scene tree for the first time.
func _ready() -> void:
	pass # Replace with function body.


# Called every frame. 'delta' is the elapsed time since the previous frame.
func _process(delta: float) -> void:
	
	pass

func get_input():
	var input_direction = Input.get_vector("left", "right", "up", "down")
	velocity = input_direction * moveSpeed

func _physics_process(delta):
	get_input()
	move_and_slide()
```
The only difference is that rather than using `Vector2`, they use `Input.get_vector()` to get user input and then use `move_and_slide()` to move the sprites based on the function `get_input()`.

To add animation, you need to first add a child note `AnimationPlayer`. Then when you click on AnimationPlayer, you can change the frame of your sprite after a certain amount of time. So I added an animation for idle for sprite's every direction and their walking animation too. 

Throughout this tinkering process, I have practiced How to Learn. By going to the GDscript documentation, I have found out that the code that was described above was outdated and therefore found another version that works for the current version of godot. For this winter break, my partners and I plan to start making the actual game by making basic mechanics of the game. We want to start by having a tilemap and then add empty spaces where then players can go there and build something. Throughout this discussion, we also practice communicating and sharing infomration to each other sharing what we have learned so we can figure out approximately how we can make this. 



Text

[Previous](entry01.md) | [Next](entry03.md)

[Home](../README.md)
