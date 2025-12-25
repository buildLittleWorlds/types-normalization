# Dataset Reference Card: Course 6 - Normalization

## Course Context

This course teaches **strong normalization** and **logical consistency** through Varen Tholl's work on proving that Sereth Linn's Calculus of Inductive Constructions terminates.

## Primary Datasets

### 1. reduction_strategies.csv

**Description**: Catalog of evaluation strategies with their properties.

**Columns**:
- `strategy_id`: Unique identifier (RS-001, RS-002, ...)
- `strategy_name`: Name of the strategy
- `description`: What the strategy does
- `reduces_which`: Which redexes it selects
- `reduces_when`: When reduction occurs
- `normalizing_behavior`: Whether it's normalizing
- `deterministic`: Whether choice is deterministic
- `used_for`: Typical applications
- `discovered_by`: Scholar who identified it
- `discovery_year`: Year of discovery
- `event_id`: Living Ledger event reference

**Key Rows**:
- RS-001: call_by_name (weak normalizing)
- RS-002: call_by_value (not normalizing for untyped)
- RS-006: full_beta (strong normalizing if typed)
- RS-012: nbe_strategy (normalization by evaluation)

**Usage Example**:
```python
strat_df = pd.read_csv(BASE_URL + "reduction_strategies.csv")
normalizing = strat_df[strat_df['normalizing_behavior'].str.contains('normalizing')]
```

---

### 2. termination_arguments.csv

**Description**: Why various type systems do or don't terminate.

**Columns**:
- `argument_id`: Unique identifier (TA-001, TA-002, ...)
- `type_system`: The type system in question
- `terminates`: Whether it terminates (true/false/semantic/conditional)
- `proof_technique`: How termination is proved
- `key_requirement`: What's needed for termination
- `why_terminates`: Explanation if it terminates
- `why_fails`: Explanation if it doesn't
- `discovered_by`: Scholar
- `discovery_year`: Year
- `event_id`: Living Ledger reference
- `reference`: Archive catalog number

**Key Rows**:
- TA-001: simply_typed_lambda (terminates via reducibility)
- TA-002: untyped_lambda (doesn't terminate - Omega)
- TA-006: cic_with_inductives (terminates with positivity)
- TA-008: type_type (doesn't terminate - Russell's paradox)

**Usage Example**:
```python
term_df = pd.read_csv(BASE_URL + "termination_arguments.csv")
terminating = term_df[term_df['terminates'] == True]
```

---

### 3. confluence_proofs.csv

**Description**: Confluence theorems and proof techniques.

**Columns**:
- `proof_id`: Unique identifier (CP-001, CP-002, ...)
- `system`: Which calculus/system
- `property`: Which property is proved
- `statement`: Formal statement
- `proof_technique`: How it's proved
- `key_lemma`: The central lemma
- `discovered_by`: Scholar
- `discovery_year`: Year
- `event_id`: Living Ledger reference
- `difficulty`: Proof difficulty rating

**Key Rows**:
- CP-001: untyped_lambda confluence (Takahashi method)
- CP-005: cic confluence (generalized reducibility)
- CP-007: normalization_confluence (unique normal forms)

**Usage Example**:
```python
conf_df = pd.read_csv(BASE_URL + "confluence_proofs.csv")
tholl_proofs = conf_df[conf_df['discovered_by'] == 'varen_tholl']
```

---

### 4. reducibility_candidates.csv

**Description**: Reducibility definitions for the normalization proof.

**Columns**:
- `candidate_id`: Unique identifier (RC-001, RC-002, ...)
- `type_constructor`: Which type constructor
- `definition`: How reducibility is defined for this type
- `closure_properties`: What properties the set satisfies
- `inhabited_by`: What terms are in the set
- `used_for`: What it's used to prove
- `discovered_by`: Scholar
- `discovery_year`: Year
- `event_id`: Living Ledger reference
- `notes`: Additional notes

**Key Rows**:
- RC-001: base_type (SN terms)
- RC-002: arrow_type (functional reducibility)
- RC-005: pi_type (dependent function reducibility)
- RC-009: inductive (positivity required)

**Usage Example**:
```python
rc_df = pd.read_csv(BASE_URL + "reducibility_candidates.csv")
dependent = rc_df[rc_df['type_constructor'].isin(['pi_type', 'sigma_type'])]
```

---

## Related Datasets

These datasets from other courses are also relevant:

- `normalization_traces.csv` (Course 3): Step-by-step reduction examples
- `curry_howard_correspondences.csv` (Course 5): Types ↔ propositions
- `typing_derivations.csv` (Course 5): Typing judgment examples

## Loading Pattern

All datasets load from the central repository:

```python
import pandas as pd

BASE_URL = "https://raw.githubusercontent.com/buildLittleWorlds/densworld-datasets/main/data/"

reduction_strategies = pd.read_csv(BASE_URL + "reduction_strategies.csv")
termination_arguments = pd.read_csv(BASE_URL + "termination_arguments.csv")
confluence_proofs = pd.read_csv(BASE_URL + "confluence_proofs.csv")
reducibility_candidates = pd.read_csv(BASE_URL + "reducibility_candidates.csv")
```

## Scholar Timeline

| Scholar | Years | Contribution | Archive Prefix |
|---------|-------|--------------|----------------|
| Brennis Mund | 780-862 | Simple type SN | MND-B |
| Arren Mott | 820-901 | Domain semantics | MOT |
| Sereth Linn | 845-928 | Dependent types | LIN |
| Varen Tholl | 895-978 | Dependent type SN | THL |

---

*Types & Computation Series - Course 6: Normalization*
