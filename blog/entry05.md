# Entry 5
##### 4/7/25

I am currently on stage 5 on Engineering Design Process, which is creating the game. 

After creating a menu to construct building, it is time for us to actually make them buildable. We created a new script that instantiate a reference of the building node that we have whenever we left click. We assigned the reference node location at mouse position so whenever the player left click it, a building will appear at where the player clicks. 

![image](https://github.com/user-attachments/assets/1c5242b3-75ab-4bc2-a00b-1d2b02602e51)

After being able to create buildings with the menu, we would need to add limitations to how buildings can be placed or else players can place buildings anywhere they want, outside of the map, on the ocean or even stacking the building. In order to fix that, we creating an array that stores all the buildings coordinates, then whenever the player place down a new building, it will look at the mouse position and loop through the array to find the closest building's coordinate. By using [`distance_to()`](https://docs.godotengine.org/en/stable/classes/class_vector2.html#class-vector2-method-distance-to), I can compare the distance between the closest building and the mouse position. If it is higher than 45 pixels, then the player can place a building there. If not, there will be a message saying that you can't place building at that location. 

An example of me trying to place a house on top of a house:
![image](https://github.com/user-attachments/assets/1b3ed9ed-9520-4d56-ab30-ad2d4d2a873a)
![image](https://github.com/user-attachments/assets/a8dd2a8a-0320-4d34-83e2-981334bb24ee)

After solving the building overlapping bug. It became a problem again when we added trees into the tilemap because the buildings can be placed on top of a trees since we only check for the building that is on the map, not trees. Therefore we would also need to find every coordinates of the trees and add them into the array. 

```gdscript
var tree_tile_ids = [2]  
	for pos in $"../trunk".get_used_cells(): 
		var tile_id = $"../trunk".get_cell_source_id(pos)
		if tile_id in tree_tile_ids:
			placed_obstacles[pos] = "trees"
```
With this code we are able to find the coordinates of every trees. However the coordinates they provide is different from the coordinates that we use the place down buildings. The coordinates that they provided are tile coordinates, meaning the coordinates are the tile location of tilemap while the coordinate we use the place down building is mouse position, measured by pixel in the viewport. Therefore if we add these tree coordinates into the array, it will give an inaccurate result because you will not be able to place building on the top left corner of the screen even though there is no tree at the top left of the screen. 

So in order to fix this issue, we need to convert the viewport coordinate to tile coordinate so that we can change the building position to tilemap coordinates to match with the trees. At first, I googled how to do that because I have no idea how you can do such things. However, all the [website](https://forum.godotengine.org/t/how-to-find-out-on-which-cell-of-tilemap-the-cursor-is-located/65242) that I have visited provides solution that are outdated. They get the actual mouse coordinate on the tilemap with `get_global_mouse_position()` and then convert it into local coordinates with `to_local()` then lastly change it to tile coordinates with `local_to_map()`. So the solution would look like this `$"../../TileMapLayer".local_to_map($"../../TileMapLayer".to_local($"../../TileMapLayer/MapCamera".get_global_mouse_position()`. However this doesn't work because `get_global_moues_position()` doesn't give you the coordinates on the entire map anymore, but rather give you the coordinates of your viewport. Therefore the coordinates that they give would be inaccurate. So eventually, I went to ask DeepSeek to see what I can do. It says that if `get_global_mouse_position()` doesn't work anymore, I can use viewport coordinate to convert to tilemap coordinates with `get_screen_transform()`. 

Eventually this chunk of code successfully converts the mouse position to tilemap coordinates:
```gdscript
$"../../TileMapLayer".local_to_map(
		$"../../TileMapLayer".to_local(
			$"../../TileMapLayer/MapCamera".get_screen_transform().affine_inverse() 
			* get_viewport().get_mouse_position()))
```

Throughout this spring break, me and my group members have worked on this project a lot and we have practice some of the skills along the way. This includes problem decomposition and embracing failure. When we are making the process of placing building. We break this task into many small parts and make it almost like a step to step guide. We started with a script that player can place down a building whenever they left click, then we change that to whenever the player click on the build house button on the menu, they can place down buildings. Then we add limitation to where buildings can be placed to prevent overlapping issues with another building and trees. The process of making this possible took us a very long time, it didn't work on the first attempt, we have to make a lot of adjustment and testing and sometimes, the errors that godot are throwing at us are extremely frustrating because we don't understand why godot are giving us this error. But we didn't give up, we keep trying and trying and eventually we step on the right track.  


[Previous](entry04.md) | [Next](entry06.md)

[Home](../README.md)
