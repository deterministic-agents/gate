# GATE - Governed Agent Trust Environment

**A cloud reference framework of controls for enterprise-grade trustworthy AI agents.**

Version: 1.3
Site: https://deterministicagents.ai
Documentation: CC BY 4.0 - Andrew Stevens · Code: MIT

---

## What is GATE?

Agentic AI systems - software that plans, retrieves context, and executes
actions with minimal human intervention - introduce a risk profile that
existing enterprise security and governance frameworks were not designed for.
Models are probabilistic, susceptible to adversarial manipulation, and capable
of taking real-world actions at machine speed.

GATE is a control-plane framework that wraps the probabilistic agent in a
deterministic shell of governance. It defines 19 controls across four layers:

| Layer | Controls | Purpose |
|---|---|---|
| Identity & Integrity | C01-C04, C17 | Prove who and what is acting; ensure runtime is untampered; discover ungoverned agents |
| Runtime Enforcement | C05-C09, C18 | Enforce policy, invariants, budgets, injection defence, and retrieval quality |
| Observability & Forensics | C10-C13, C19 | Produce evidence, replayability, non-repudiation, and behavioural drift detection |
| Orchestration & Ecosystem | C14-C16 | Govern distributed and multi-agent autonomy safely |

**The core invariant:** agent runtimes never call tools or memory directly.
All side effects traverse deterministic enforcement points that authenticate,
authorise, constrain, and record every action.

---

## Downloads

### Framework paper

The canonical reference for the framework. Includes the threat model,
4-layer architecture, all 19 controls (Why/What/How/Evidence/Failure Modes),
control plane contracts overview, cloud quickstarts (AWS/Azure/GCP), and
standard mappings to NIST AI RMF and ISO/IEC 42001.

**[Download GATE v1.3 (PDF)](https://assets.whitepaper.download/gate/v1.3/a262eccc-8196-481c-bd83-14b018b2a1d4/Governed%20Agent%20Trust%20Environment%20(GATE)%20v1.3.pdf)**

SHA-256: `8a31d97577b957cc3de18b213fd0b13ba739570ee12d7d5f69da222776ecd186`

### Artifacts bundle

Everything in one zip: schemas, Rego policies, ABOM templates, conformance
checks, SQL queries, operational runbooks, and the Python reference library.

**[Download GATE-artifacts-v1.1.zip](https://github.com/deterministic-agents/gate/releases/download/v1.3/GATE-artifacts-v1.1.zip)**

SHA-256: `d80104ea3218d8e2943e32fb7465cc5f6600548e9e6c7817d51106a52c1a5d6b`

---

## Implementation repositories

Each component is a separate versioned repository. Clone what you need.

| Repository | Version | Purpose |
|---|---|---|
| [gate-contracts](https://github.com/deterministic-agents/gate-contracts) | v1.1.0 | JSON Schema contracts for all GATE control plane events. The canonical dependency - start here. |
| [gate-python](https://github.com/deterministic-agents/gate-python) | v1.1.0 | Python reference library: hashing, envelopes, ledger, replay, signing, schema validation, plus v1.3 discovery / memory.quality / assurance.behaviour modules. |
| [gate-policies](https://github.com/deterministic-agents/gate-policies) | v1.1.0 | OPA/Rego baseline policy bundle, invariant bundle (C09), unit tests, ABOM templates, plus v1.3 c17 / c18 / c19 policies. |
| [gate-conformance](https://github.com/deterministic-agents/gate-conformance) | v1.1.0 | 19 conformance checks, self-assessment template, evidence SQL queries, 9 operational runbooks. |

---

## Versioning

| Artefact | Version | Notes |
|---|---|---|
| Framework paper (PDF) | v1.3 | Current release |
| HTML spec | v1.1 | C17/C18/C19 entries, Check16-19 must-pass summary, portrait diagrams |
| gate-contracts | v1.1.0 | Six new event schemas; five new resource schemas |
| gate-python | v1.1.0 | gate.discovery, gate.memory.quality, gate.assurance.behaviour |
| gate-policies | v1.1.0 | c17_discovery, c18_quality, c19_drift_response (new files only) |
| gate-conformance | v1.1.0 | Check16-Check19; 7 v1.3 queries; RB-07/08/09 |

The framework paper version is independent of the implementation repo versions.
Release notes for each version are in the [Releases](https://github.com/deterministic-agents/gate/releases) tab.

---

## Changelog

**v1.3** - Three new controls extending GATE's scope to cover assumptions that
v1.2.8 left implicit. C17 Agent Discovery and Shadow AI Detection (Layer 1):
continuous discovery of ungoverned agents and enrol-or-terminate path feeding
C04. C18 Data Quality Gates (Layer 2): retrieval-time freshness, confidence,
and provenance gates at the Memory Gateway. C19 Model Behaviour Monitoring
(Layer 3): continuous statistical drift detection against a signed baseline,
held distinct from C16 adversarial validation. Check16-Check19 added. Six new
control plane contract schemas. Three new Rego policy files. Three new Python
modules. Explicit scope statements for the shadow AI assumption, memory
quality boundary, and C16/C19 event type distinction. C04 lifecycle gains a
Discovered entry state. GATE namespace replaces DARE throughout contracts.

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

Documentation, schemas, and policies: CC BY 4.0 - Andrew Stevens
Code (gate): MIT
Required attribution for CC content: "Governed Agent Trust Environment (GATE)"
by Andrew Stevens, licensed under CC BY 4.0. Source: deterministicagents.ai
