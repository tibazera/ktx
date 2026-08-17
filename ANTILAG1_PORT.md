# Antilag 1 port scope

This branch ports the existing Dusty Antilag 1 behaviour to current
QW-Group/KTX.  It is not a new game mode and it does not change the
semantics of `sv_antilag 1`: players retain the current opt-in Antilag 1
behaviour, including hitscan correction, simple projectiles, weapon
prediction, accurate timing and the matching CSQC program.

## Explicit non-goals

This branch must not add player spray decals or any spray protocol support.
In particular it must not add `sprays.c`, `sv_sprays.c`, `clc_spray`,
`svc_spray`, `MVD_PEXT1_SPRAYS`, `G_SPRAY*`, or a spray cvar.

Sprays, if ever proposed, are a later opt-in feature series on top of the
finished Antilag 1 port.  They must be independently build-gated and disabled
by default.  Antilag 1 must remain complete and usable without them.

## Porting rules

* Start from current QW-Group/KTX rather than merging a downstream tree.
* Port only changes required for Antilag 1 and its matching CSQC support.
* Keep each logical protocol, server and CSQC change reviewable in its own
  commit where practical.
* Build `qwprogs.so` and `csprogs.dat` from the same source revision.
* Keep normal Antilag 0/2 behaviour unchanged when `sv_antilag` is not 1.
