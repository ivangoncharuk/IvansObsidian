#godot 
## Introduction to Shaders

### What are Shaders?
- Special programs that run on GPUs.
- Initially for shading 3D scenes, now for various tasks.
- Control how the engine renders geometry and pixels.

### How do they work?
- Process in parallel.
- Operate on each vertex or pixel in isolation.
- Cannot store data between frames.

#### GDScript vs Shaders
```gdscript
# GDScript
for x in range(width):
  for y in range(height):
    set_color(x, y, some_color)

# Shader
void fragment() {
  COLOR = some_color;
}
```

## Shaders in Godot

### Godot's Shading Language
- Based on GLSL but simplified.
- Handles low-level initialization.
- Written with "processor functions."

### Processor Functions
1. `vertex()`: Runs for all vertices in a mesh.
2. `fragment()`: Runs for every pixel covered by mesh.
3. `light()`: Runs for every pixel and light.
4. `start()`: Runs for every particle at spawn.
5. `process()`: Runs for every particle each frame.
6. `sky()`: Runs for every pixel in radiance cubemap and screen.
7. `fog()`: Runs for every froxel in fog buffer.

> ⚠️ **Warning**: `light()` function won't run if vertex lighting is enabled.

- There is an API available for writing completely custom GLSL shaders.

## Shader Types in Godot

### Specification
- Specify shader type at the beginning.
```gdscript
shader_type spatial;
```

### Types
1. `spatial`: For 3D rendering.
2. `canvas_item`: For 2D rendering.
3. `particles`: For particle systems.
4. `sky`: To render skies.
5. `fog`: To render FogVolumes.

## Render Modes in Godot

### Specification
- Optional and specified after shader type.
```gdscript
shader_type spatial;
render_mode unshaded, cull_disabled;
```

### Purpose
- Alter how Godot applies the shader.
  
#### Note
- Each shader type has its own set of render modes.

## Vertex Processor

### Functionality
- Called once for each vertex.
- Modifies vertex properties like position, color.
- Can pass extra data to `fragment()` using `varyings`.

#### Note
- Default transformations are handled by Godot but can be overridden.

## Fragment Processor

### Functionality
- Runs per pixel.
- Sets up material properties like `ROUGHNESS`, `RIM`, `TRANSMISSION`.
  
#### Note
- If properties are not used, Godot optimizes them away.

## Light Processor

### Functionality
- Runs per pixel, per light.
- Affects material properties set in `fragment()`.
  
#### Note
- Works differently in 2D and 3D. Check respective documentation.

---

Feel free to let me know if you would like to add more to this or modify any section.