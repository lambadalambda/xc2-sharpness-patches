001 Eden Sharp Graphics (Xenoblade Chronicles 2, v2.1.0)
========================================================
Companion to "002 Eden 1080p Scene". Built/tested 2026-07-05.

lib_nx.ini is read natively by the Monolith engine from romfs/stream/dumpini/
(developer override path) — no exefs patch needed, plain LayeredFS.

Changes vs. stock:
  AntiAliasing=off     (from the community AA-killer baseline)
  tmaa=off             kill the TMAA smear (720p-tuned temporal AA)
  TransReduction=off   full-resolution transparency (hair, effects)
  trans_red_scl X/Y=1.0
  ColReduction=off     full-resolution color/effect buffers
  shadowHalf=off       full-resolution shadow filtering
  red_Auto=off         (note: red_* keys appear inert on XC2; the
                        "Disable Resolution Scaling" pchtxt does this in code)

If distant edges shimmer in motion, set AntiAliasing=on and AA_Sharpness=0.3.
