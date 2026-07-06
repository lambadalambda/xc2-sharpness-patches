002 Eden 1080p Scene (Xenoblade Chronicles 2, v2.1.0)
=====================================================
THE key sharpness fix. Built/tested 2026-07-05.

XC2 renders its 3D scene at 1280x720 but composites into a 1920x1080 output
framebuffer — every frame passes through a fractional (1.5x) bilinear resample.
That resample is scale-invariant: no matter what internal resolution multiplier
the emulator uses (3x, 5x, ...), the last hop stays a 1.5x bilinear smear,
which is why raising the emulator resolution never made the game look sharp.

This pchtxt sets the scene resolution to 1920x1080 == output framebuffer, so
the composite becomes 1:1 and the emulator multiplier scales a clean pipeline.
Measured ~4-6x fine-detail energy at 3x (Laplacian variance on fixed crops).

Derived from emoose's 1440p patch for v2.1.0
(https://gist.github.com/emoose/93a81ff4944933cafe64160a91f2acbe):
  MOVZ W21,#1920 -> 006FFDC0 15F08052   (was #2560 in the 1440p patch)
  MOVZ W22,#1080 -> 006FFDC4 16878052   (was #1440)
nsobid F77F1559371C0EC6D50E78774AC59D95 matches this dump's main.

Use together with "001 Eden Sharp Graphics" (kills TMAA + half-res buffers).
With scene==output, ANY emulator multiplier is clean — use 2x if 3x is too heavy.
emoose noted minor map/cutscene effect quirks with resolution patches; report
anything that looks off.
