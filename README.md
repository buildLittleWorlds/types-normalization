# Course 6: Normalization

*Strong Normalization and Logical Consistency through Varen Tholl's Normalization Discipline*

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/buildLittleWorlds/types-normalization/blob/main/notebooks/01-why-normalization-matters.ipynb)

> "He proved passages reach their end" — Varen Tholl's epitaph

## Course Overview

This course teaches **strong normalization** and its relationship to **logical consistency** through the story of Varen Tholl (895-978), who proved that Sereth Linn's Calculus of Inductive Constructions terminates.

Where Course 5 (Dependent Classifications) showed how types can express propositions, this course shows why termination matters: if every well-typed term reduces to a value, then the type system cannot prove False. Normalization is the bridge from computation to logic.

## Prerequisites

- Course 3: Typed Passages (understanding of simple types)
- Course 5: Dependent Classifications (dependent types, Curry-Howard)

## Learning Objectives

By the end of this course, you will be able to:

1. Explain why normalization matters for logical consistency
2. Distinguish strong from weak normalization
3. State and prove the confluence (Church-Rosser) property
4. Apply the reducibility method to prove normalization
5. Explain why structural recursion and positivity are required
6. Connect normalization to logical consistency via Curry-Howard
7. Describe normalization by evaluation (NbE)

## Tutorials

| # | Title | Topic | Technical Content |
|---|-------|-------|------------------|
| 01 | Why Normalization Matters | The stakes | Type-checking, consistency, Curry-Howard |
| 02 | Reduction and Normal Forms | Computation | Redexes, strategies, values |
| 03 | Confluence | Uniqueness | Church-Rosser, diamond property |
| 04 | Reducibility Candidates | Proof technique | Logical relations, closure properties |
| 05 | Termination and Recursion | Safety | Structural recursion, positivity |
| 06 | Consistency from Normalization | Soundness | Empty type, progress |
| 07 | The Normalization Discipline | Synthesis | Tholl's framework, NbE |

## The Scholar: Varen Tholl

**Varen Tholl** (895-978) was born the same year Sereth Linn discovered the Curry-Howard correspondence. He joined the Capital Archives in Year 920 — the year Linn published her final synthesis — and studied under her for three years before her retirement.

After observing that type-level computation could diverge, Tholl launched a systematic investigation into normalization. Over 50 years, he developed:

- The reducibility method for dependent types
- Confluence proofs for the CIC
- The positivity requirement for inductive types
- The consistency theorem (normalization implies logical soundness)
- Normalization by evaluation

Key milestones:
- **930**: Distinguishes strong from weak normalization
- **932**: Proves confluence for CIC
- **945**: Develops reducibility candidates for dependent types
- **952**: Proves normalization implies consistency
- **955**: Publishes normalization proof for CIC
- **962**: Proposes normalization by evaluation
- **970**: Publishes "The Normalization Discipline"

## Technical Concepts

### Strong Normalization

A term M is **strongly normalizing** if every reduction sequence starting from M terminates:

```
M → M₁ → M₂ → ... → v  (reaches value)
```

No matter which redex you reduce, you eventually reach a normal form.

### Confluence (Church-Rosser)

If M reduces to N₁ and M reduces to N₂, there exists N₃ such that both N₁ and N₂ reduce to N₃:

```
      M
     / \
    ↓   ↓
   N₁   N₂
    \   /
     ↓ ↓
      N₃
```

### Reducibility Candidates

For each type A, define CR(A) = "reducible terms of type A":

```
CR(Nat) = { M : Nat | M strongly normalizes }
CR(A → B) = { M : A → B | ∀N ∈ CR(A). M N ∈ CR(B) }
CR(Π(x:A).B) = { M | ∀N ∈ CR(A). M N ∈ CR(B[N/x]) }
```

### Consistency from Normalization

**Theorem**: If all well-typed terms normalize, the type system is consistent.

**Proof**: Suppose M : Empty (the type with no constructors). By normalization, M reduces to a canonical form. But Empty has no constructors, so no canonical form exists. Contradiction.

## Datasets

This course uses four datasets:

| Dataset | Description |
|---------|-------------|
| `reduction_strategies.csv` | Evaluation strategies (call-by-name, call-by-value, etc.) |
| `termination_arguments.csv` | Why various type systems terminate or not |
| `confluence_proofs.csv` | Confluence theorems and proof techniques |
| `reducibility_candidates.csv` | Reducibility definitions for each type constructor |

## Living Ledger Integration

This course contributes **24 canonical events** to the Living Ledger, spanning Varen Tholl's career from 895-979.

Key events:
- EV-895-010: Tholl born
- EV-932-003: Confluence proved
- EV-945-005: Reducibility candidates developed
- EV-952-004: Consistency from normalization
- EV-978-003: Tholl dies

## How to Use This Course

Each notebook can be run in Google Colab. Click the badge at the top of each notebook to launch:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)

## Connection to Other Courses

- **Course 3** (Typed Passages): Simple types and Brennis's normalization proof
- **Course 4** (Continuous Domains): Semantic foundations (Mott)
- **Course 5** (Dependent Classifications): Linn's CIC, what Tholl normalizes
- **Course 7** (Equivalence via Passage): Keth's homotopy type theory (next)

## The Critic: Corvin Gast

**Corvin Gast** (fourth generation of the Gast family of critics) objected that normalization cannot be proved within the system it normalizes (echoing Gödel). Tholl's response: we prove normalization *about* the CIC in a metatheory, not *within* the CIC. The trust chain is explicit.

## Repository

This course is part of the [densworld-courses](https://github.com/buildLittleWorlds) project.

---

*Types & Computation Series*
*buildLittleWorlds*
