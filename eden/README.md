# Eden texture-cache patches (emulator-side)

Two patches for the [Eden](https://eden-emu.dev) emulator's texture cache that
complement the mods in this repo. They keep XC2's sub-scene-resolution effect
buffers (half-res post-process buffers, and the fixed 720p water/env buffers
that appear once the 1080p scene patch is active) at native resolution, so the
game's integer `texelFetch` composites sample them correctly — without them,
high internal-resolution multipliers show a dark rectangle grid and a vertical
center seam (originally across whole scenes; with the 1080p mod, on water /
wet areas).

- `0001` — exclude XC2's sub-720p color render targets from rescaling
  (fixes the original scene-wide grid/seam with the vanilla 720p scene)
- `0002` — infer the scene height from the largest widescreen depth buffer
  instead of hardcoding 720, so the exclusion also covers the fixed 720p
  buffers when the scene is patched to 1080p

Scoped to XC2's title ID (`0100E95004038000`) — no other game is affected.

## Applying

```sh
git clone https://git.eden-emu.dev/eden-emu/eden   # or your fork
cd eden
git am /path/to/xc2-sharpness-patches/eden/*.patch
```

Then build as usual. Written against Eden master @ `4c65780f11` (2026-07);
the touched functions (`TextureCache::ImageCanRescale` and the member block in
`texture_cache_base.h`) change rarely, so they should apply cleanly for a while.
