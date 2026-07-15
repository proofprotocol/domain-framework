# Proof Protocol™ Domain Framework

**Document ID:** PP-SPEC-012  
**Version:** 1.0  
**Status:** Published  
**License:** CC BY 4.0  
**Maintained by:** Proof Economy™ Standards Alliance (PESA)  
**Repository:** https://github.com/proofprotocol  
**Published:** 2026-07-14  

---

## Abstract

This specification defines the ten domains of the Proof Protocol™ Domain Framework. Each domain addresses a distinct category of independently verifiable proof. Together they constitute the organizational structure of the Proof Economy™ — the complete set of things that must be proven, not claimed, about a system operating under adversarial conditions.

---

## Status of This Document

Published specification of the Proof Protocol™. CC BY 4.0 — attribution to Craig Ellrod / Nebulonium, Inc. / HACKERverse required.

---

## 1. Introduction

The Proof Protocol™ Domain Framework answers a question no other published standard addresses: what are the complete categories of proof that an AI security system must produce to be trusted at scale?

Existing frameworks answer adjacent questions. Taxonomies name what can go wrong. Governance frameworks define what controls should exist. Regulations mandate outcomes. None of them define what proof of those controls looks like, or organize that proof into a coherent domain structure.

This specification does that. The ten domains are not a checklist. They are a framework for organizing proof requirements across the full lifecycle of adversarial AI security — from pre-execution commitment through post-execution auditability.

### 1.1 Relationship to Other PP-SPECs

Each domain in this framework is implemented by one or more existing PP-SPEC specifications. This document is the organizing layer — it defines what each domain means and why it matters. The referenced specifications define how to implement it.

### 1.2 Scope

This specification defines the ten domains, their definitions, their core questions, and their key mechanisms. It does not define conformance requirements for individual domains — those are defined in the implementing specifications.

---

## 2. The Ten Domains

### Domain 01 — Containment

**Core question:** Did the system stay within defined boundaries during execution?

**Definition:** Independently verifiable proof that actions, data, and agent behaviors stayed within defined boundaries during execution.

**Why it matters:** Containment is the most fundamental proof requirement. Logs cannot answer the containment question — they are produced by the system being observed. Containment proof requires an independent witness operating outside the subject's trust boundary.

**Key mechanism:** AgenTwin™ witnesses execution from outside the agent trust boundary, assembling proof that the subject operated within authorized parameters.

**Implementing specifications:** PP-SPEC-001, PP-SPEC-005

---

### Domain 02 — Efficacy

**Core question:** Did security controls actually work under adversarial conditions?

**Definition:** Independently verifiable proof that security controls actually worked under adversarial conditions, expressed as a numeric score.

**Why it matters:** Efficacy is the only domain with a published formula. PES (Proof of Efficacy Score) = Blocked / (Blocked + Missed) × 100. OBSERVED and IRRELEVANT cases are excluded from the denominator. A product that cannot produce a PES score under adversarial conditions has not been tested — it has been described.

Efficacy is the domain no other published standard defines as of 2026-07-14. It is the commercial forcing function of the Proof Economy™: buyers will ask for a score. Only a ProofStamp™-certified run produces one.

**Key mechanism:** PES formula applied to Arena7™ execution results, witnessed by AgenTwin™, sealed by ProofProtocol.

**Reference implementation:** Pipelock v3.0.0 — PR-2026-00028 — PES 99.2%, Detection 100%, FP 4.5%, 164 applicable cases.

**Implementing specifications:** PP-SPEC-001, PP-SPEC-006

---

### Domain 03 — Integrity

**Core question:** Was the system tampered with before, during, or after the benchmark run?

**Definition:** Independently verifiable proof that a system's execution environment, configuration, and outputs were not tampered with before, during, or after the benchmark run.

**Why it matters:** Integrity proof begins with the NIST Randomness Beacon pre-execution commitment. Because the pulse cannot be predicted, any commitment made before execution cannot have been fabricated after the fact. Integrity is the structural property that makes retroactive falsification impossible — not merely detectable, but impossible.

**Key mechanism:** NIST Randomness Beacon pre-execution commitment. The pulse index, timestamp, and output value are recorded before execution begins. Post-hoc fabrication of a proof artifact requires predicting a future Beacon pulse — which is cryptographically infeasible.

**Implementing specifications:** PP-SPEC-001, PP-SPEC-002, PP-SPEC-008

---

### Domain 04 — Attribution

**Core question:** Who or what authorized each action at each step of execution?

**Definition:** Independently verifiable proof of who or what authorized each action, at each step of execution, including delegated authority chains.

**Why it matters:** In agentic AI systems, attribution is the hardest accountability problem. An agent acting on behalf of a human principal, delegating to a subagent, which calls a tool — each step must be independently attributable. Without attribution proof, accountability is a fiction.

**Key mechanism:** PP-A2P™ defines proof requirements at each delegation boundary. Each agent-to-agent interaction requires proof exchange before trust is established. The delegation chain is assembled into the ProofBundle™.

**Implementing specifications:** PP-SPEC-007, PP-SPEC-005

---

### Domain 05 — Provenance

**Core question:** Where did this proof come from, and can the chain be independently verified?

**Definition:** Independently verifiable proof of the origin, lineage, and custody chain of a proof artifact — from raw execution data through ProofBundle™ assembly to ProofRegister™ submission.

**Why it matters:** Provenance closes the fabrication window. If a proof artifact cannot demonstrate an unbroken chain of custody from NIST Beacon commitment through witnessed execution through sealed submission, it is not a proof artifact. It is a document.

**Key mechanism:** PP-SPEC-011 defines the provenance record structure, pre-execution commitment procedure, lineage requirements, and chain of custody events.

**Implementing specifications:** PP-SPEC-008, PP-SPEC-011

---

### Domain 06 — Portability

**Core question:** Can anyone verify this proof anywhere, without access to proprietary infrastructure?

**Definition:** Independently verifiable proof that the proof artifact is self-contained, independently verifiable without access to proprietary infrastructure, and portable across vendors, platforms, and jurisdictions.

**Why it matters:** A ProofBundle™ is verifiable offline. No ProofRegister™ access required. No HACKERverse account required. No vendor relationship required. This is the property that makes ProofStamp™ certification meaningful to a regulator, insurer, or court — they do not need to trust the infrastructure. They need to verify the bundle.

**Key mechanism:** PP-SPEC-003 defines the ProofBundle™ format as a self-contained artifact. All verification inputs — NIST Beacon pulse, commitment hash, witness attestation, execution records — are embedded in the bundle.

**Implementing specifications:** PP-SPEC-003, PP-SPEC-008

---

### Domain 07 — Continuity

**Core question:** Does the security posture hold over time, or only at the moment of certification?

**Definition:** Independently verifiable proof that security posture holds across time — not just at the moment of certification, but through ongoing adversarial execution on cadence.

**Why it matters:** Continuity is what separates a certification mark from a certificate. A certificate is issued once. A ProofStamp™ lapses when continuous execution stops. The lapse condition is not a restriction on the mark — it is the mark. A certification that does not expire when the threat landscape moves has measured a moment and sold it as a state.

**Key mechanism:** ProofStamp™ lapse condition. Every certified build carries an expiry. The mark lapses on that date unless a subsequent run has executed and published. Execution stops, the assertion stops.

**Implementing specifications:** PP-SPEC-009

---

### Domain 08 — Adversariality

**Core question:** Was the system actually attacked, or just described as having been tested?

**Definition:** Independently verifiable proof that a system was tested under real adversarial conditions — not synthetic inputs, not vendor-controlled scenarios, not self-reported results.

**Why it matters:** Adversariality is the domain that invalidates the entire existing framework landscape. Every taxonomy names adversarial techniques. Every governance framework requires adversarial testing. Every regulation mandates adversarial resilience. None of them execute the adversary.

Adversariality is the proof that the attack actually ran — witnessed independently, committed to NIST Beacon, sealed on-chain. No other published standard defines Adversariality as a proof domain as of 2026-07-14.

**Key mechanism:** Arena7™ executes adversarial TTPs under NIST Beacon pre-execution commitment. AgenTwin™ witnesses from outside the trust boundary. Results are sealed in ProofRegister™. The proof is the execution record, not a description of it.

**Implementing specifications:** PP-SPEC-001, PP-SPEC-005, PP-SPEC-006

---

### Domain 09 — Auditability

**Core question:** Can a regulator, insurer, buyer, or court verify this proof without vendor access or privilege?

**Definition:** Independently verifiable proof that any third party can verify the proof record without access to proprietary systems, vendor relationships, or privileged infrastructure.

**Why it matters:** Auditability is the property that converts a proof artifact into legal and regulatory evidence. A ProofBundle™ is verifiable by anyone with the bundle and the NIST Beacon public API. The Bitcoin OP_RETURN anchor is verifiable on any block explorer. The ProofRegister™ record is publicly queryable by PCID. No gate. No account. No vendor permission required.

**Key mechanism:** Public ProofRegister™ queryable by PCID. Bitcoin OP_RETURN on-chain anchor verifiable on any block explorer. NIST Beacon pulse verifiable at beacon.nist.gov. No proprietary verification infrastructure required.

**Implementing specifications:** PP-SPEC-003, PP-SPEC-004, PP-SPEC-008, PP-SPEC-010

---

### Domain 10 — Causality

**Core question:** What caused what — across the full chain of agent actions and downstream effects?

**Definition:** Independently verifiable proof of the chain between an agent action and its downstream effects — what authorized action A, what A caused, what B authorized as a result, and what B caused in turn.

**Why it matters:** Causality is the domain that emerges from agentic AI at scale. When an autonomous agent executes thousands of actions in a pipeline, the question is not just what happened — it is what caused what. Without causality proof, post-incident investigation is reconstruction, not evidence.

AgenTwin™ witnesses the full execution chain from outside the agent trust boundary, assembling receipts, pubkeys, and verifier output at each step. The ProofBundle™ is the causal chain, sealed and independently verifiable.

Causality is the domain that makes AI accountable at the depth regulators and insurers will eventually require. No other architecture produces it.

**Key mechanism:** AgenTwin™ assembles the full causal chain across agent-to-agent interactions. PP-A2P™ requires proof exchange at each step, creating a verifiable record of what authorized what.

**Implementing specifications:** PP-SPEC-007, PP-SPEC-005, PP-SPEC-011

---

## 3. Domain Summary

| # | Domain | Core Question | Key Mechanism |
|---|--------|--------------|---------------|
| 01 | Containment | Did it stay in bounds? | Independent witness outside trust boundary |
| 02 | Efficacy | Did it actually work? | PES — Blocked / (Blocked + Missed) × 100 |
| 03 | Integrity | Was it tampered with? | NIST Beacon pre-execution commitment |
| 04 | Attribution | Who authorized what? | PP-A2P™ delegation chain proof |
| 05 | Provenance | Where did this proof come from? | Custody chain from commitment to seal |
| 06 | Portability | Can anyone verify this anywhere? | Self-contained offline-verifiable ProofBundle™ |
| 07 | Continuity | Does it hold over time? | ProofStamp™ lapse condition |
| 08 | Adversariality | Was it actually attacked? | Arena7™ execution under NIST Beacon commitment |
| 09 | Auditability | Can a third party verify independently? | Public ProofRegister™ + Bitcoin OP_RETURN |
| 10 | Causality | What caused what? | AgenTwin™ full chain witness assembly |

---

## 4. Exclusive Domains

**Domain 02 — Efficacy** and **Domain 08 — Adversariality** have no equivalent in any published AI security standard as of 2026-07-14.

No other standard defines a numeric efficacy metric for security control performance under adversarial conditions. No other standard defines adversarial execution as a proof domain. These are the two domains that make the Proof Protocol™ structurally irreplaceable in the Proof Economy™.

---

## 5. Relationship to the Broader Landscape

The Proof Protocol™ Domain Framework is not a competitor to existing AI security frameworks. It is the proof layer that sits underneath all of them.

Every governance framework tells a system what controls to implement. Every taxonomy tells a system what threats exist. Every regulation mandates outcomes. The Proof Protocol™ Domain Framework defines what proof of those controls, against those threats, satisfying those outcomes, looks like.

The frameworks name the categories. The Proof Protocol™ proves them.

---

## 6. Authors

Craig Ellrod, Founder & CEO, Nebulonium, Inc. (d/b/a HACKERverse)  
Castle Rock, Colorado  
2026-07-14

---

*CC BY 4.0 — Attribution to Craig Ellrod / Nebulonium, Inc. / HACKERverse required.*
