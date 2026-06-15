Fix blender 2.49b NIFscripts 2.5.9 Oblivion creature export crashes

- Replace collisonobject for creatures (flags=1)
- Add default NiTransformController+Interpolator to bones without IPO
- Disable skin partition
- Preserve NiTexturingProperty for glow materials
- Set collision layer via object property instead of global option

6/11/26: Line 3138 — Fixed Matrix33 crash in export_bones. Changed interp.rotation.x = node.rotation.x etc. to use node.rotation.get_scale_quat() which correctly converts the rotation matrix to a quaternion.
Line 2628 — Added a call to trishape._pre_reduce_vertex_weights(4) before update_bind_position() and update_skin_partition(). This pre-reduces each vertex to at most 4 bone influences (with renormalization) so the partition creation doesn't need to drop any bones itself — preventing the "Lost vertex weights" crash.
"Bin\Blender\pyffi\formats\nif\underscore_underscore_init_underscore_underscore.py": 3. Line 6835 — Added the new _pre_reduce_vertex_weights() method to the NiGeometry class.
Bin\Blender\.blender\scripts\bpymodules\nif_common.py: 4. Line 362 — Changed EXPORT_BONESPERPARTITION default from 18 to 32 5. Line 872 — Updated GUI slider max from 18 to 32 6. Line 1381 — Updated Oblivion/FO3 game defaults to use BONESPERPARTITION=32

6/15: 
- Import seams and "glowing nostrils" from split normals (import_nif.py)
  NIF files with split-per-face normals imported with hard-edge seams.
  Added IMPORT_MERGE_VERTICES_BY_POSITION option to use position-only dedup
  and recalculate smooth normals from faces.

Changed
-------
- EXPORT_BONESPERPARTITION default raised 18 -> 32 (nif_common.py)
- GUI slider max updated 18 -> 32
- Oblivion/FO3 game defaults updated to match

Added
-----
- Bone Renamer script (object/object_niftools_rename_bones.py)
  Renames bones from a .txt mapping file. Supports comma-separated sources,
  prefix matching (pelvis matches pelvis_1, pelvis_2_1, etc.), updates
  vertex groups and animation channels.
  Format: pelvis, pants = Bip01 Pelvis

- Import GUI toggle: "Merge Vertices By Position (Fix Seams)"

Files
-----
.\.blender\scripts\export\export_nif.py
.\pyffi\formats\nif\__init__.py
.\.blender\scripts\bpymodules\nif_common.py
.\.blender\scripts\import\import_nif.py
.\.blender\scripts\object\object_niftools_rename_bones.py

Usage
-----
How to use; Locate Blender 2.49 scripts folder (e.g., Blender2.49\Bin\Blender\) use the folders in update there
Download modified version and overwrite.

Particles still don't work, iirc there was a civ4 script where it does, might be an idea for a future update.

All credit to the Nifskope team, this is just a small patch for a very old tool for an even older gamee
