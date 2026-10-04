# Rule-Based Expert System (Project 2)

A Python expert system that accepts user-selected symptoms, applies IF-THEN rules with **forward chaining**, and displays its reasoning path.

> **Safety note:** This is an educational programming demonstration, not a medical device or diagnostic tool. Its simplified rules are not clinically validated. It must not be used to make treatment decisions.

## Features

- Facts base: stores the symptoms supplied by the user.
- Rule base: contains ten IF-THEN rules.
- Inference engine: repeatedly applies rules until no new facts can be inferred.
- Multi-step inference: intermediate conclusions can activate later rules.
- Explanation log: displays which rule fired, its conditions, and its conclusion.
- Handles no-match cases without crashing.
- Command-line and optional Flask web interfaces.

## Project structure

```text
rule_based_expert_system/
├── engine.py
├── knowledge_base.py
├── cli.py
├── app.py
├── requirements.txt
├── README.md
└── tests/
    └── test_engine.py
```

## Requirements

- Python 3.10 or newer
- Flask is only needed for the web interface.

## Run the command-line version

```bash
python cli.py
```

Answer each symptom prompt with `y` or `n`. The program prints the inferred conclusions and every fired rule.

## Run the web version

```bash
pip install -r requirements.txt
python app.py
```

Open http://127.0.0.1:5000 in your browser, select symptoms, and click **Run Expert System**.

## Run tests

```bash
python -m unittest discover -s tests -v
```

## How forward chaining works

1. The user provides initial facts (selected symptoms).
2. The engine checks every rule's IF conditions against the known facts.
3. If all conditions match, the rule fires and its THEN conclusion is added as a new fact.
4. That new fact may satisfy another rule, creating a multi-step chain.
5. The process stops when a complete pass adds no new facts.
6. The engine returns all facts and the inference log.

## Example multi-step test

Initial facts:

```text
fever, cough, fatigue, body_aches, high_fever
```

Reasoning:

```text
R1: fever AND cough AND fatigue
    -> viral_pattern

R4: viral_pattern AND body_aches AND high_fever
    -> possible_influenza_pattern
```

This demonstrates that the conclusion from R1 becomes an input condition for R4.

## Customizing the system

Add a `Rule` entry in `knowledge_base.py`. Each rule needs:
- a unique name,
- a set of required conditions,
- a conclusion fact,
- a short explanation.

The generic engine in `engine.py` does not need to change when you add domain rules.
