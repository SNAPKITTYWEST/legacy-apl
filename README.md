# LEGACY-APL — SOVEREIGN APL CORRECTIONS

> Pure APL proofs of domain orthogonality, entropy isolation, and contractive stability. No Python. No wrappers. No MLIR. Just APL and the WORM chain.

This repository is the **APL proof substrate** of the SNAPKITTYWEST sovereign-compute constellation. Extracted from the `all-apl` workspace, it collects pure-APL corrections and demonstrations that establish sovereign-domain isolation and PIRTM/Ω-correctness as *structural facts*, not policy rules.

## WHAT IT IS

`legacy-apl` is a collection of self-contained APL modules plus the metadata/state model that anchors them to the Bifrost WORM chain. Every module is written in idiomatic APL (index origin 1, `⍝` comments) and runs in a plain APL session — no host-language glue.

Core themes proven in APL:

- **INTERCOL** — sovereign domain orthogonality: distinct domains are orthogonal vectors; cross-domain transition returns `⊥` (Null State). Includes the PIRTM `transition_108_cycle` collapse proof.
- **Domain isolation** — the "mathematical wall": no asset from domain A can reach domain B.
- **Ω isolation** — local uncertainty/entropy `I%` must be strictly below bound `Ic`.
- **PIRTM stability** — finite-gain contraction certificate; spectral radius `< 1` required.
- **Morphism composition** — correct `f∘g` order.
- **Zeroproof substrate** — refutes literal proof hashes and tautological factorization claims.
- **Transforms** — Fibonacci/phinary contraction, entropy mapping, trust-vector reduction, semantic-agreement fold (feeds the INTERCOL Swift/C++ UI via JSON).

## ARCHITECTURE / COMPONENTS

| Path | Purpose |
|------|---------|
| `README.md` | Repo marker (Apache-2.0, extracted from all-apl). |
| `apl-corrections/` | The pure-APL proof modules (see below). |
| `apl-corrections/metadata.json` | Sealing metadata: `MATHLIB5-20260710-APLCORRE-001`, SHA-256 tamper chain, AES-256-GCM, Ed25519 Plasma Gate, Bifrost WORM provenance, `awaiting_worm_seal`. |
| `apl-corrections/state-model.json` | INTERCOL UI runtime state: 7-axis EDAULC trust vector, 5-pass ERE gates, 13-node Metatron resonance graph, WORM receipt schema (append-only: append \| verify \| replay). |
| `docs/generate-docs.mjs` | Continuous docs generator (`.rs .lean .py .apl .hs .mjs .js .pl .md`); `--watch` mode; auto git-commit/push. |
| `docs/README.md` | Usage note for the generator. |
| `theorems/THEOREMS.md` | Local theorem pointer (full list in `theorems` repo index). |

### APL proof modules (`apl-corrections/`)

| File | Proves |
|------|--------|
| `intercol.apl` | `INTERCOL` inner product, orthonormality, Null-State transition, PIRTM 108-cycle collapse, sovereign isolation. |
| `sovereign_domain.apl` | Domain boundary encoding (`name lower upper omega cap`). |
| `omega_isolation.apl` | `I% < Ic` isolation boundary. |
| `pirtm_stability.apl` | Finite-gain contraction certificate (spectral radius `< 1`). |
| `morphism_composition.apl` | Correct `(f Compose g) x = f(g(x))` order. |
| `zeroproof_substrate.apl` | Refutes literal proof hashes / tautological factorization. |
| `transforms.apl` | Phinary/Fibonacci transforms + trust-vector/semantic folds for the UI. |
| `run_all.apl` | `RunAll` demo runner wiring the modules together. |

A shared primitive appears across modules: `Assert` (guard + `⎕SIGNAL 11`) and `BOB` (proof-step checker) — the APL analogue of a verifier witness.

## HOW IT FITS THE CONSTELLATION

`legacy-apl` is the **structural-correctness witness layer**:

- **WORM Chain / Bifrost** — `metadata.json` chains each correction to `Bifrost_WORM_Chain_20260710_01`; `state-model.json` defines the append-only WORM receipt schema.
- **Plasma Gate (Ed25519)** — `security_audit.plasma_gate: "Ed25519_Enforced"`; tamper evidence is a SHA-256 append-only chain.
- **P/NP Swarm** — the `BOB`/`Assert` proofs are P-verifiable certificates; swarm agents submit witnesses that a domain really is isolated.
- **3-Witness Verification** — a sovereign-domain claim is accepted only after three independent APL runs reproduce the `⊥` Null State.

> **Ω ← TRUST ∧ CODE**: a domain wall holds only when the Ed25519/WORM trust ∧ the APL `INTERCOL = 0` code both verify.

Related repos: `handoff` (continuity), `theorems` (central index where `legacy-apl` is tracked).

## BUILD / USAGE / INSTALL

No build. Requires an APL interpreter (e.g. GNU APL, Dyalog).

```bash
cd legacy-apl

# Load the proof modules in an APL session, then:
)LOAD apl-corrections/run_all.apl
RunAll                         ⍝ runs all demos, returns stability/domain/omega/zero/morphism

# Generate/refresh docs:
node docs/generate-docs.mjs          # one-shot
node docs/generate-docs.mjs --watch  # continuous; auto-commits + pushes
```

`run_all.apl` expects `⎕IO←1` and the `src` modules loaded first (see `state-model.json` `intercol_state._apl_source`).

## KEY FILES REFERENCE

- **`apl-corrections/intercol.apl`** — the centerpiece: orthonormal domain space, `DomainTransition` returning `⊥` on cross-domain, and `PIRTMCollapseProof` showing `transition_108_cycle = ⊥` by construction.
- **`apl-corrections/metadata.json`** — `review_status: human_review_required`, `split` across 9 layers (audit, kernel, proofs, runtime, witnesses, refinements, asp_gate, fol_engine, prism_skills).
- **`apl-corrections/state-model.json`** — 13-node Metatron resonance graph, 7-axis EDAULC trust vector, entropy gate threshold `0.21`, WORM receipt schema.

## LICENSE

Apache-2.0.
