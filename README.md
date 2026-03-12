# The Ormle Standard (v1.0)
**A Formal Foundation for Semantic Data Representation and Machine-Reasoning**

[cite_start]The Ormle Standard addresses the "Semantic Gap" in modern data architecture[cite: 5]. [cite_start]While SQL DDL describes how data is stored, it remains silent on what that data actually means[cite: 5, 6, 7]. [cite_start]This specification provides a semantic layer that bridges physical metadata (DDL) and the conceptual schema required for deterministic machine reasoning[cite: 3, 9].

## Key Concepts
* [cite_start]**Fact-Based Modeling**: Represents a database as a collection of Fact Types—binary relations expressed as natural-language readings[cite: 8, 13, 14].
* [cite_start]**Deterministic Constraints**: Formalizes uniqueness and mandatoriness as logical laws that govern join semantics and functional dependencies[cite: 54, 56, 57, 59].
* [cite_start]**Role-Based Identity**: Uses Reference Schemes to identify preferred join keys, eliminating the "guesswork" typical of LLM-based text-to-SQL generation[cite: 20, 25, 26].
* [cite_start]**Ontological Rigor**: Enables automated systems to distinguish between physical storage and conceptual facts[cite: 64, 65, 66].

## Implementation
[cite_start]The standard is serialized as a JSON document[cite: 79, 96]. [cite_start]You can find the normative schema definition in this repository as `ormle-spec-v1.0.json`[cite: 79].

## Full Specification
For the formal foundation—including the predicate calculus, notation, and normative comparisons—view the full documentation at:
**[ormle.com/Standard](https://www.ormle.com/Standard)**
