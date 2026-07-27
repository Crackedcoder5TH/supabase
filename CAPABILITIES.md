# Supabase — Verified Capabilities (Remembrance Ecosystem Fork)

This repo's piece of the [ecosystem](../Void-Data-Compressor/CAPABILITIES.md).

Last verified: 2026-04-30, branch `claude/audit-remembrance-ecosystem-xaaUr`.

---

## Role in ecosystem

Forked Supabase used as the persistence / data backend for
ecosystem state that needs durability beyond local files. Not
yet integrated into the cross-repo introspection pass — does
not currently appear in the `cross_repo_function_records.json`
substrate (no `repo='supabase'` entries).

This is **deliberate**: the substrate scorer indexes ecosystem-level
function records. Supabase Studio is its own large React/TypeScript
codebase with ~thousands of files; folding it into the same
substrate would dwarf the rest. Supabase here serves the
ecosystem as a backend, not as a participant in the scoring pass.

---

## ✅ Verified — what's NOT promised

| # | Capability | Test |
|---|---|---|
| 1 | Supabase records are **not** in cross-repo records | `python3 -c "import json; d=json.load(open('../Void-Data-Compressor/cross_repo_function_records.json')); repos=set(r['repo'] for r in d['records']); print('supabase' in repos)"` → False |
| 2 | No `REPO_ROOTS['supabase']` in void-side scripts | `grep -l "'supabase'" ../Void-Data-Compressor/*.py` returns nothing |

This is the correct state. Adding supabase to the substrate would
require a deliberate integration choice with appropriate scoping
rules (which directories, which file types).

---

## What this repo does on its own

It's a Supabase fork. See `README.md` for the upstream feature set.

The standards that apply to **integration with the remembrance
ecosystem** (when supabase functions ARE used by other repos):

- Pattern publication: any supabase-side code that exposes data to
  other ecosystem repos should be addressable via `coh://` URI when
  registered (see oracle `node src/cli.js register --file ...`)
- Coherency gate: any pattern submitted from supabase via the oracle
  CLI passes the same covenant validator and 0.60 minimum gate

---

## ❌ Out of scope here

- The 77k-pattern substrate — void
- Multi-layer coherency scoring — void
- Atomic table / covenant — oracle
- Cascade simulation — void

---

*Cross-cutting capabilities: see [`Void-Data-Compressor/CAPABILITIES.md`](../Void-Data-Compressor/CAPABILITIES.md).*
