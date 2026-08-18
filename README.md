# GATE - Governed Agent Trust Environment

**A cloud reference framework of controls for enterprise-grade trustworthy AI agents.**

Version: 1.4
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
deterministic shell of governance. It defines 20 controls across four layers:

| Layer | Controls | Purpose |
|---|---|---|
| Identity & Integrity | C01-C04, C17 | Prove who and what is acting; ensure runtime is untampered; discover ungoverned agents |
| Runtime Enforcement | C05-C09, C18 | Enforce policy, invariants, budgets, injection defence, and retrieval quality |
| Observability & Forensics | C10-C13, C19, C20 | Produce evidence, replayability, non-repudiation, behavioural drift detection, and validated agent-to-human output |
| Orchestration & Ecosystem | C14-C16 | Govern distributed and multi-agent autonomy safely |

**The core invariant:** agent runtimes never call tools or memory directly.
All side effects traverse deterministic enforcement points that authenticate,
authorise, constrain, and record every action.

---

## Downloads

### Framework paper

The canonical reference for the framework. Includes the threat model,
4-layer architecture, all 20 controls (Why/What/How/Evidence/Failure Modes),
control plane contracts overview, cloud quickstarts (AWS/Azure/GCP), and
standard mappings to NIST AI RMF, ISO/IEC 42001, OWASP AISVS, MITRE ATLAS,
and NIST SSDF.

**[Download GATE v1.4 (PDF)](https://github.com/deterministic-agents/gate/releases/download/v1.4/GATE-v1.4.pdf)**

The HTML specification at [deterministicagents.ai](https://deterministicagents.ai/) and a single-file markdown export (`GATE-v1.4.md`, attached to the v1.4 release) carry the same content.

SHA-256: `a6719e946a166e4b9cae7a7de1ebb001ed190ab18ebd6cb2340ebe77d463f2a8`

### Artifacts bundle

Everything in one zip: schemas, Rego policies, ABOM templates, conformance
checks, SQL queries, operational runbooks, and the Python reference library.

**[Download GATE-artifacts-v1.4.zip](https://github.com/deterministic-agents/gate/releases/download/v1.4/GATE-artifacts-v1.4.zip)**

SHA-256: `ece601f4d674f5daecc1303c701573b3fd7302a71da6a72d2e61d4d0e73a4714`

---

## Implementation repositories

Each component is a separate versioned repository. Clone what you need.

| Repository | Version | Purpose |
|---|---|---|
| [gate-contracts](https://github.com/deterministic-agents/gate-contracts) | v1.2.0 | JSON Schema contracts for all GATE control plane events. The canonical dependency - start here. v1.2.0 adds the C20 output classification, break-glass record, auto-enrolment policy, and approved feed registry schemas. |
| [gate-python](https://github.com/deterministic-agents/gate-python) | v1.2.0 | Python reference library: hashing, envelopes, ledger, replay, signing, schema validation, plus v1.4 gate.output (C20) and break-glass modules and the cross-language canonical JSON vectors. |
| [gate-policies](https://github.com/deterministic-agents/gate-policies) | v1.2.0 | OPA/Rego baseline policy bundle, invariant bundle (C09), unit tests, ABOM templates, plus v1.4 c20 output classification, c09 break-glass verification, and c17 auto-enrolment policies. |
| [gate-conformance](https://github.com/deterministic-agents/gate-conformance) | v1.3.0 | 20 conformance checks plus the conformance runner. Automates 9 checks against your evidence store (11 with bundle stores configured). Self-assessment template, evidence SQL queries, 9 operational runbooks, AISVS / ATLAS / SSDF mappings. |
| [gate-rust](https://github.com/deterministic-agents/gate-rust) | v1.0.0 | Rust companion crate: canonical JSON, envelopes, ledger, ES256 signing. Hash-compatible with gate-python via the shared cross-language test vectors. |
| [gate-fuzz](https://github.com/deterministic-agents/gate-fuzz) | v1.0.0 | Hypothesis-based Python-to-Rust differential property suite covering canonical JSON, signing, and schema validation parity. |
| [gate-knowledge](https://github.com/deterministic-agents/gate-knowledge) | v1.0.0 | The GATE conceptual layer as an Open Knowledge Format (OKF) v0.1 bundle: controls, threat model, architecture layers, adoption path, ABOM template. |

---

## Versioning

| Artefact | Version | Notes |
|---|---|---|
| Framework paper (PDF) | v1.4 | Current release |
| HTML spec | v1.1 | C17/C18/C19 entries, Check16-19 must-pass summary, portrait diagrams |
| gate-contracts | v1.2.0 | Four new schemas (C20, break-glass, auto-enrolment, feed registry); AutoEnrolled state; control catalog v1.2 |
| gate-python | v1.2.0 | gate.output (C20), break-glass module, strict hashing, cross-language vectors + CI |
| gate-policies | v1.2.0 | c20_output_classification, c09_break_glass_verification, c17_auto_enrolment, bundle manifest |
| gate-conformance | v1.3.0 | Check20, Check17/18 conditional automation, AISVS + ATLAS + SSDF mappings |
| gate-rust | v1.0.0 | First release: canonical JSON, envelopes, ledger, ES256 signing |
| gate-fuzz | v1.0.0 | First release: Python-to-Rust differential property suite |
| gate-knowledge | v1.0.0 | First release: OKF v0.1 knowledge bundle |

The framework paper version is independent of the implementation repo versions.
Release notes for each version are in the [Releases](https://github.com/deterministic-agents/gate/releases) tab.

---

## Changelog

**v1.4** - One new control and three tightened controls. C20 Agent-to-Human
Output Validation (Layer 3): per-response classification at the delivery
boundary with configurable redact / review / hold obligations, fail-closed
at high_privilege tier. C09 gains a signed break-glass record contract with
dual approval. C17 gains an automated enrolment fast-path backed by a signed
policy contract. C18 provenance now chains back to a registered source or an
approved external feed. Check20 added; Check17 and Check18 upgrade from
PARTIAL to AUTOMATED when bundle stores are configured. AISVS, ATLAS, and
SSDF standard mappings added. Three new repositories: gate-rust (Rust
companion crate, hash-compatible with gate-python), gate-fuzz (cross-language
differential property suite), and gate-knowledge (the conceptual layer as an
OKF v0.1 bundle). Artifacts bundle rebuilt as GATE-artifacts-v1.4.zip.

**v1.3.1** (2026-06-16) - Implementation repo Releases complete.
Conformance runner shipped in gate-conformance v1.2.0
(`python -m runner.cli`). Patch releases on gate-contracts (v1.1.1)
and gate-policies (v1.1.1) clean up README staging artefacts; schema
and policy content unchanged from v1.1.0. Artifacts bundle rebuilt as
GATE-artifacts-v1.2.zip with the v1.2.0 conformance runner included.
No framework-paper changes.

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
