# GATE - Governed Agent Trust Environment

**A cloud reference framework of controls for enterprise-grade trustworthy AI agents.**

Version: 1.2.8  
Site: https://deterministicagents.ai  
Documentation: CC BY 4.0 — Andrew Stevens · Code: MIT

---

## What is GATE?

Agentic AI systems - software that plans, retrieves context, and executes
actions with minimal human intervention - introduce a risk profile that
existing enterprise security and governance frameworks were not designed for.
Models are probabilistic, susceptible to adversarial manipulation, and capable
of taking real-world actions at machine speed.

GATE is a control-plane framework that wraps the probabilistic agent in a
deterministic shell of governance. It defines 16 controls across four layers:

| Layer | Controls | Purpose |
|---|---|---|
| Identity & Integrity | C01–C04 | Prove who and what is acting; ensure runtime is untampered |
| Runtime Enforcement | C05–C09 | Enforce policy, invariants, budgets, and injection defence |
| Observability & Forensics | C10–C13 | Produce evidence, replayability, and non-repudiation |
| Orchestration & Ecosystem | C14–C16 | Govern distributed and multi-agent autonomy safely |

**The core invariant:** agent runtimes never call tools or memory directly.
All side effects traverse deterministic enforcement points that authenticate,
authorise, constrain, and record every action.

---

## Downloads

### Framework paper

The canonical reference for the framework. Includes the threat model,
4-layer architecture, all 16 controls (Why/What/How/Evidence/Failure Modes),
control plane contracts overview, cloud quickstarts (AWS/Azure/GCP), and
standard mappings to NIST AI RMF and ISO/IEC 42001.

**[Download GATE v1.2.8 (PDF)](https://github.com/deterministic-agents/gate/releases/download/v1.2.8/Governed%20Agent%20Trust%20Environment%20(GATE)%20v1.2.8.pdf)**

SHA-256: `7b10a35831d018da2032642a9bd396ce20d816a09ac9121d9eec74a2332ca8db`

### Artifacts bundle

Everything in one zip: schemas, Rego policies, ABOM templates, conformance
checks, SQL queries, and operational runbooks.

**[Download GATE-artifacts-v1.0.zip](https://github.com/deterministic-agents/gate/releases/download/v1.2.8/GATE-artifacts-v1.0.zip)**

---

## Implementation repositories

Each component is a separate versioned repository. Clone what you need.

| Repo | Version | What it is |
|---|---|---|
| [gate-contracts](https://github.com/deterministic-agents/gate-contracts) | v1.0.0 | JSON Schema contracts for all GATE control plane events. The canonical dependency - start here. |
| [gate-python](https://github.com/deterministic-agents/gate-python) | v1.0.0 | Python reference library: hashing, envelopes, ledger, replay, signing, schema validation. |
| [gate-policies](https://github.com/deterministic-agents/gate-policies) | v1.0.0 | OPA/Rego baseline policy bundle, invariant bundle (C09), unit tests, ABOM templates. |
| [gate-conformance](https://github.com/deterministic-agents/gate-conformance) | v1.0.0 | 15 conformance checks, self-assessment template, evidence SQL queries, 6 operational runbooks. |

**Dependency direction:** `gate-contracts` ← everything else. Start with
contracts, then add the layer you are implementing.

---

## HTML specification

The framework is also published as a browsable HTML specification at
[deterministicagents.ai/spec.html](https://deterministicagents.ai/spec.html),
including the full control catalog with filtering and framework mappings.

---

## Where to start

**If you are a platform or cloud architect:**  
Read the framework paper. Then clone `gate-contracts` and `gate-python` to
understand the enforcement boundary contracts.

**If you are a security engineer:**  
Start with `gate-policies`. The Rego baseline and invariant bundle are
deployable with OPA. The tool authorization matrix and ABOM examples show
how to model your agent fleet.

**If you are a GRC analyst or auditor:**  
Start with `gate-conformance`. The self-assessment YAML maps each check
to a test procedure and evidence requirement. The conformance report template
is ready to fill in.

**If you are making the case to executives or a CISO:**  
Read the [Trustworthy Agentic AI Blueprint](https://www.sakurasky.com/white-papers/trustworthy-agentic-ai-blueprint/)
first. It covers the strategic case and 4-layer architecture that GATE
implements. GATE is the engineering companion to the Blueprint.

---

## Adoption path

GATE is designed to be adopted in phases. Don't try everything at once.

**Phase 1 - Establish the execution boundary** (minimum viable control plane)  
C01 · C03 · C05 · C06 · C07 · C08 (baseline) · C11  
Exit criteria: zero tool calls without a policy decision record; zero bypass paths.

**Phase 2 - Make incidents reproducible and defensible**  
Add: C08 (full depth) · C10 · C12 · C13  
Exit criteria: replay reproduces high-impact runs; signed-action coverage at target.

**Phase 3 - Govern distributed and multi-agent autonomy**  
Add: C14 · C15 · C16  
Exit criteria: multi-agent messages validated; safe rollout enforced.

---

## Versioning

| Artefact | Version | Notes |
|---|---|---|
| Framework paper (PDF) | v1.2.8 | Current release |
| HTML spec | v1.0 | Initial |
| gate-contracts | v1.0.0 | Stable |
| gate-python | v1.0.0 | Stable |
| gate-policies | v1.0.0 | Stable |
| gate-conformance | v1.0.0 | Stable |

The framework paper version is independent of the implementation repo versions.
Release notes for each version are in the [Releases](https://github.com/deterministic-agents/gate/releases) tab.

---

## Changelog

**v1.2.8** - Renamed from DARE to GATE (Governed Agent Trust Environment).
C09 rewritten as Execution Constraints and Invariant Enforcement with
hardened invariant bundle, break-glass override semantics, and approval
fatigue failure mode. C08 split across Phase 1 (deterministic controls)
and Phase 2 (probabilistic controls) in the adoption path. ORM Risk Model
Worksheet (Artifact A7) now includes tuning guidance and deployment context
table. Conformance runner roadmap note added. Azure and GCP quickstart
parity improved.

---

## License

Documentation, schemas, and policies: CC BY 4.0 — Andrew Stevens  
Code (gate): MIT  
Required attribution for CC content: "Governed Agent Trust Environment (GATE)"  
by Andrew Stevens, licensed under CC BY 4.0. Source: deterministicagents.ai
