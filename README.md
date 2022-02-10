## Overview

Shader collection for sprites in Godot. In version 0.1, plugins has 20+ shader.

If you have experience with shader and just want to refer to some shader, you can find file.shader in:
res://addons/godot_sprite_shader/assets/shader/

If you are not experience about shader or just want to use them in a few simple cases, this plugin comes with SShader (Sprite Shader) that help you use shader and run their animation quickly. You don't need config the noise texture for the shader, everything is already config, you just drag and drop the type shader you want to use and change param it.


![Preview](https://github.com/duongvituan/godot-sprite-shader/blob/master/preview_image/preview_demo.gif)
![Use](https://github.com/duongvituan/godot-sprite-shader/blob/master/preview_image/demo_use.gif)

## Install and use

Watch tutorial video: update late


### Installation
Copy the contents of folder addons in plugins to your project and activate GodotSpriteShader.

If you need more details, you can watch the video above.



### How to use GodotSpriteShader
1. First, you need to add Node SShaderContainer and set the "node path" to the node where you want to use the shader (it can be Sprite, RectTexturem ViewportContainer...)
2. Add the SShader types you want to use. The SShader is child of SShaderContainer.
3. Use:
 - With SShader you can activate or inactive them to apply or remove shader into the sprite.
 - With SShaderInterval (orange) types it needs to update the process_value variable to do the animation, you can do this with the AnimationPlayer or using the functions:
 
```
func play(duration: float, inactive_when_finished: bool = false):
func play_repeat(duration: float, repeat: int, inactive_when_finished: bool = false, delay_each_repeat: float = 0.0):
func play_repeat_forever(duration: float, delay_each_repeat: float = 0.0):

func play_reverse(duration: float, inactive_when_finished: bool = false):
func play_reverse_repeat(duration: float, repeat: int, inactive_when_finished: bool = false, delay_each_repeat: float = 0.0):
func play_reverse_repeat_forever(duration: float, delay_each_repeat: float = 0.0):
```

ex: ```$Char2/SShaderContainer/SSDissolveDust.play(1.0, false)```

Note: 
If you call function play for the SShader (White), it's simply an active shader at the start and inactive shader at the end.

ex: You want to create a flash effect - "hit effect" when the character is hit.

Pseudocode:
- Active Shader change Sprite to white color.
- Wait 0.1s
- Inactive Shader

The code when you use SShader for above example:
```
    $SShaderContainer/SSOneColor.play(0.1, true)
```

![Hit Effect](https://github.com/duongvituan/godot-sprite-shader/blob/master/preview_image/hit_effect.gif)

### Use Viewport

- All SShaders work fine when you use shaders with textures of 1 image.
- However, some SShader do not work well when sprites use a sheet image.

The way to fix this is to use Viewport:

 #### Create :
- Select the Sprite or Node you want to import in the Viewport.
- In the GSS Extensions section. You can enter the size and press OK Button.

![Create](https://github.com/duongvituan/godot-sprite-shader/blob/master/preview_image/use_viewport.gif)

#### Update:
- To update the size of Viewport, you select ViewportContainer, then adjust the size and click Update Button.

![Update](https://github.com/duongvituan/godot-sprite-shader/blob/master/preview_image/update_viewport.gif)

Note: this tool "add node to Viewport" is still in testing so it may not work as expected.
If you have a problem with this tool then you can create a pull to help me fix it or create an issue and I will fix it late.


### Using multiple shaders:
- You can create more viewports to use (each viewport use 1 shader)
![MultipleShader](https://github.com/duongvituan/godot-sprite-shader/blob/master/multi_shader/update_viewport.gif)


## QA:
### I got the sprite_language.cpp error message when I installed the plugin:
```core/script_language.cpp:232 - Condition "!global_classes.has(p_class)" is true. Returned: String()```
You may get this error when first time install plugin.
I don't know why, but you can close and reopen the project to fix error :(.


### Shaders behave unexpectedly:
- If you are using Sprite with Sheets image then you need to use viewport.
- If you use Viewport make sure SShaderContainer has node path to ViewportContainer not for Sprite. Check that the old shader file is still in the sprite, delete it if you used it in the viewport.


## Contribution
Contributions are welcome and are accepted via pull requests.

You can contribute code and submit pull or you can provide ideas and resources by creating an issue. :)


## License

[MIT License](https://github.com/duongvituan/godot-sprite-shader/blob/master/LICENSE)

