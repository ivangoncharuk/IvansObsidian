---
tags:
  - godot
---

#### General Concepts
- Skeletons have Position/Rotation/Scale (Transform) tracks linked to bones.
- Bones can have different Transform values even if they share names.
- Skeletons use "Bone Rest" for the default pose.
- Godot 4.0+ includes Bone Rest in the Bone Pose, unlike Godot 3.x.
- Different 3D models have different Bone Rests depending on the export environment.
  
#### Sharing Animations
- To share animations, both Bone Rests and Bone Names must match.
- Use the scene importer in Godot 4.0+ to manage this.

#### Retargeting Options

##### Bone Map
- Select `Skeleton3D` node for "Retarget" section with a property called `bone_map`.
- Setup a new BoneMap and SkeletonProfile, e.g., `SkeletonProfileHumanoid`.
- Auto-mapping is enabled; manual mapping is also possible.
- Errors in mapping are highlighted but don't block the import.

##### Remove Tracks
- Recommended for shared AnimationLibrary.
- Different options like `Except Bone Transform`, `Unimportant Positions`, and `Unmapped Bones` for selective track removal.

##### Bone Renamer
- `Rename Bones` to rename mapped bones.
- `Unique Node` option allows unifying animation track paths.

##### Rest Fixer
- Rules for reference poses, like T-pose, axis directions, and joint bending.
- `Apply Node Transform` fixes issues with wrongly exported models.
- `Normalize Position Tracks` adjusts stride lengths for different model heights.
- `Overwrite Axis` forcefully aligns Bone Rests to match reference poses.
  
##### Fix Silhouette
- Helps match model's silhouette to reference poses.
- Specifically useful for T-pose to A-pose adjustments.
- Options for excluding bones from adjustment and height adjustments via `base_height_adjustment`.

##### Code Example for Filters
```python
# To specify bones you don't want fixed
filter_array = ["BoneName1", "BoneName2"]
```

##### Notes
- Auto-mapping works best with common English bone names.
- Some options can affect other objects in the scene negatively.
- Use Realtime Retarget Module if original Bone Rests are crucial.