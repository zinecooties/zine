# Dependency submodules

Wuffs, SuperMD, and SuperHTML are submodules pinned to upstream commits.
The small local changes are stored in `vendor/zig-master.patch`, rather
than unpublished commits in the submodules.

After cloning Zine, run from its root:

```sh
git submodule update --init --recursive
git apply vendor/zig-master.patch
z17 build
```

The patch remains applied in the submodule working trees, so Git reports
them as modified. Apply it once per clean checkout. Before changing the
submodule revisions, reverse it with `git apply -R vendor/zig-master.patch`,
then update and refresh the patch as needed.

Wuffs and SuperMD only change `build.zig.zon`, to share the root package's
Zig 0.17-compatible translate-c and local SuperHTML copy.

| Package | Upstream revision | Original package hash |
| --- | --- | --- |
| Wuffs build wrapper | https://github.com/allyourcodebase/wuffs/commit/364ba880b20ca1c9b94ee41b07738bc941cee275 | `wuffs-0.4.0-alpha.9+3837.20240914-3CHJgY8LAADueYEeHrj8cQs_rZQ0bDGsngrbgV7Z2LFt` |
| SuperMD | https://github.com/kristoff-it/supermd/commit/d3aabca3315fe82b3addb3b9a2e16e2388ff7f4d | `supermd-0.1.0-3Mco3Fa_WACwtQyvM7f-cZigRV6Ac2f4ahvdcYmU_PhD` |
| SuperHTML | https://github.com/kristoff-it/superhtml/commit/23ef2f44ca0df2d2e05a0be3874370553c5b591d | `superhtml-0.7.0-Y7MdPHKkJgA1s7ycx0okrfwclJaChKuAbTrsjmQ3uGlM` |

SuperHTML changes only two calls in `src/template.zig`: `getLast()` becomes
`last()` to preserve optional empty-stack handling under Zig master.

Wuffs' C source remains a fetched dependency. The SuperMD and SuperHTML
licenses are retained in their respective directories.
