#godot 

## Description

- Tweens are mostly useful for **animations** requiring a numerical property to be interpolated over a range of values. 
- The name _tween_ comes from *in-betweening*, an animation technique where you specify _keyframes_ and the computer interpolates the frames that appear between them. 
- Animating something with a **Tween** is called `tweening`.

---

- Tween is better when you don't know the end values for an animation in advance.
- Tween is good for animations like dynamically adjusting camera zoom, which would be hard with AnimationPlayer.
- Tween is more resource-efficient compared to AnimationPlayer.
- Tween is suitable for simple animations and tasks that don't require visual adjustments via an editor.
- Tween can be used for one-off logic, like making something shoot periodically using a looped CallbackTweener with a delay.

---

A **Tween** can be created by using either 

`SceneTree.create_tween()` 
or
`Node.create_tween`

- **Tween**s created manually (i.e. by using `Tween.new()`) are invalid and can't be used for tweening values.

> A tween animation is created by adding tweeners to the **Tween** object, using 
> - [tween_property](https://docs.godotengine.org/en/stable/classes/class_tween.html#class-tween-method-tween-property), 
> - [tween_interval](https://docs.godotengine.org/en/stable/classes/class_tween.html#class-tween-method-tween-interval), 
> - [tween_callback](https://docs.godotengine.org/en/stable/classes/class_tween.html#class-tween-method-tween-callback) or 
> - [tween_method](https://docs.godotengine.org/en/stable/classes/class_tween.html#class-tween-method-tween-method)

---

## Example

```python
var tween = get_tree().create_tween()
tween.tween_property($Sprite, "modulate", Color.RED, 1)
tween.tween_property($Sprite, "scale", Vector2(), 1)
tween.tween_callback($Sprite.queue_free)
```

This sequence will make the `$Sprite` node 
1. turn red, 
2. then shrink, 
3. before finally calling `Node.queue_free` to free the sprite. 

5. Tweeners are executed one after another by default. This behavior can be changed using 
	- [parallel](https://docs.godotengine.org/en/stable/classes/class_tween.html#class-tween-method-parallel) and 
	- [set_parallel](https://docs.godotengine.org/en/stable/classes/class_tween.html#class-tween-method-set-parallel).

When a Tweener is created with one of the `tween_*` methods, a chained method call can be used to tweak the properties of this [Tweener](https://docs.godotengine.org/en/stable/classes/class_tweener.html#class-tweener). For example, if you want to set a different transition type in the above example, you can use [set_trans](https://docs.godotengine.org/en/stable/classes/class_tween.html#class-tween-method-set-trans):


[[How to use ERDs]]
