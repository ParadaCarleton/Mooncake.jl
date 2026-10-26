# `enhanced`

ParadaCarleton's build of Mooncake.jl: chalk-lab/Mooncake.jl `main` plus the pull requests
from this fork that `main` does not contain yet. Our projects load this branch's head.

Order (steps 1-4 each fast-forward the one before; later steps merge into the branch):

1. chalk-lab `main` at 61128b2 ("Rules for Base._unsetindex! on MemoryRef", #1352; includes #1334).
2. `forward-rule-copy` up to ac4a80f: chalk-lab/Mooncake.jl#1357, `build_frule` returns a copy of
   a cached derived rule (7ce005f, afd4f2d, and the merge of `main` in ac4a80f).
3. `world-carry-pr`: carry derived rules across world moves that invalidate nothing they depend on
   (38b262d, 88608a9, 881124d, and the formatting commit on top).
4. This file.
5. A merge of chalk-lab `main` (v0.5.65).
6. A merge of `friendly-array-input`: chalk-lab/Mooncake.jl#1366, forward mode accepts array
   tangents of another array type (1ddc8b2, 526cd8f).
7. A merge of `shared-forward-rules` (6f300598, on chalk-lab `main` b00fb6a): a derived forward
   rule without per-call state is shared rather than copied. With step 3, a cache fetch shares one
   copy rebased to the fetching world (`shared_rule_at`), made on that world's first fetch.

Left out: `scopedvalue-zero-derivative` (#1346, one commit 1dc9f89, closed unmerged). A zero
derivative for reading a `ScopedValue` is wrong whenever the scoped value depends on the input, so
the maintainers closed it in favour of #1348, which refuses ScopedValue access; #1348 is open and
not in `main`.

Left out: `compile-latency`, `compile-latency-c2`, `compile-latency-c2only` (153a4c3, 54867ba,
d88525a): compile-time experiments, abandoned after a 2.4x warm-solve regression.

`irv` (the fork's earlier branch) is ac4a80f, covered by step 2.
