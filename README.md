# Daily Reflection Tree — Deterministic Agent

## Overview

This project implements a deterministic end-of-day reflection system as part of the DT Fellowship assignment.

The system guides an employee through a structured reflection across three psychological axes:

1. **Locus (Victim vs Victor)** — identifying agency in outcomes
2. **Orientation (Contribution vs Entitlement)** — focusing on what was given vs expected
3. **Radius (Self vs Others)** — expanding perspective beyond self

The reflection is implemented as a **decision tree**, not an AI system.

---

## Key Principles

* **Deterministic**
  Same inputs always produce the same outputs. No randomness.

* **No LLM at Runtime**
  The system does not call any AI model during execution.

* **Fixed Options Only**
  All user inputs are predefined choices. No free-text input.

* **Structured Reasoning**
  Each response updates internal state using signals (e.g., axis1:internal).

---

## Project Structure

```
dt-reflection/
 ├── tree/
 │    └── reflection-tree.yaml     # Core decision tree
 ├── write-up.md                  # Design explanation
 └── README.md                    # Project overview
```

---

## Tree Design

The reflection flow is divided into three sequential axes:

### Axis 1: Locus (Control)

Evaluates whether the user attributes outcomes to internal actions or external factors.

### Axis 2: Contribution

Measures whether the user focused on contributing value or expecting returns.

### Axis 3: Radius

Determines whether the user’s perspective remained self-centered or extended to others.

Each axis contains:

* Questions with fixed options
* Signals attached to options
* Reflections based on accumulated signals

---

## Node Types

* **start** — begins the session
* **question** — user selects from fixed options
* **decision** — routes based on previous answers
* **reflection** — provides insight based on path
* **bridge** — transitions between axes
* **summary** — synthesizes user behavior
* **end** — closes session

---

## State & Signals

Each answer contributes to internal state:

* `axis1:internal` / `axis1:external`
* `axis2:contribution` / `axis2:entitlement`
* `axis3:self` / `axis3:others`

The final summary is generated using:

* Dominant signals
* Stored answers (via interpolation)

---

## How to Use

1. Load the YAML file
2. Traverse nodes sequentially
3. At each question:

   * Display options
   * Capture selection
4. Update state using signals
5. Follow deterministic branching
6. Display summary at end

---

## Notes

* This project focuses on **knowledge structuring**, not UI or AI
* The quality of the system depends on the **clarity of questions and branching logic**
* The tree is designed to simulate a reflective conversation without ambiguity

