# Entry 2
##### 12/15/24

I am currently on stage 2 on Engineering Design Process, which is researching tool, I continued watching [Michael Game Tutorial](https://www.youtube.com/playlist?list=PLfcCiyd_V9GH8M9xd_QKlyU8jryGcy3Xa) and so far I have learned how I can play around with godot settings such as viewport, sprites graphic, and adding user input into input mapping so godot will observe this inputs. I also learned how I can create a GDScript to code a sprite's movement and add animation when the sprites are moving. 

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
Basically what this code is doing is that we get inputs from user with `get_input()` and then in function `_physics_process()` we call `move_and_slide()` to get the sprite moving according to the user's input. 



Text

[Previous](entry01.md) | [Next](entry03.md)

[Home](../README.md)
