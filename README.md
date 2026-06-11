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

How to use; Locate Blender 2.49 scripts folder (e.g., Blender2.49\Bin\Blender\.blender\scripts\export\)

Backup original export_nif.py, underscore_underscore_init_underscore_underscore.py, and nif_common.py

Download modified version and overwrite.

Particles still don't work, iirc there was a civ4 script where it does, might be an idea for a future update.

All credit to the Nifskope team, this is just a small patch for a very old tool for an even older gamee
