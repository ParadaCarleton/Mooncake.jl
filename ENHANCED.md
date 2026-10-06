# `enhanced`

ParadaCarleton's build of Mooncake.jl: chalk-lab/Mooncake.jl `main` plus the pull requests
from this fork that `main` does not contain yet. Our projects pin a commit of this branch.

Order (each step is a fast-forward of the one before it):

1. chalk-lab `main` at 61128b2 ("Rules for Base._unsetindex! on MemoryRef", #1352; includes #1334).
2. `forward-rule-copy` up to ac4a80f: chalk-lab/Mooncake.jl#1357, `build_frule` returns a copy of
   a cached derived rule (7ce005f, afd4f2d, and the merge of `main` in ac4a80f).
3. `world-carry-pr`: carry derived rules across world moves that invalidate nothing they depend on
   (38b262d, 88608a9, 881124d, and the formatting commit on top).
4. This file.

Left out: `scopedvalue-zero-derivative` (#1346, one commit 1dc9f89, closed unmerged). A zero
derivative for reading a `ScopedValue` is wrong whenever the scoped value depends on the input, so
the maintainers closed it in favour of #1348, which refuses ScopedValue access; #1348 is open and
not in `main`.

`irv` (the fork's earlier branch) is ac4a80f, covered by step 2.
