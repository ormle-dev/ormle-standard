# Ormle Knowledge Graph Specification (v1.0)
**A Formal Foundation for Semantic Data Representation and Machine-Reasoning over Relational Structures**

**Status:** Published  ·  **Category:** Technical Specification  ·  **Publisher:** Ormle  ·  **Date:** March 2026

---

### Abstract
This document defines the **Ormle Knowledge Graph Specification (v1.0)**, a formal standard for representing relational database schemas as collections of **Asserted Predicates** rather than physical storage descriptors. The specification provides a semantic layer that bridges the gap between physical database metadata (DDL) and the conceptual schema required for deterministic machine reasoning.

---

### 1. Introduction: The Semantic Gap
Modern large language models (LLMs) exhibit systematic failure in text-to-SQL tasks because SQL Data Definition Language (DDL) constitutes physical metadata: it describes how data is stored, not what it means. A column definition such as `CustomerID INT NOT NULL` is a physical constraint; it provides no semantic information about the role that `CustomerID` plays in the business domain. 

The Ormle Standard addresses this deficiency by representing a database as a collection of **Fact Types**—binary relations expressed as natural-language readings—augmented with formally defined constraints. This representation allows an LLM to read the schema rather than infer it, moving from stochastic interpretation to deterministic reasoning.

---

### 2. Definitions and Notation

#### 2.1 Entities and Value Types
Let $E$ denote the set of all **Entity Types** and $V$ denote the set of all **Value Types**.
* An **Entity Type** represents a non-value object in the domain (e.g., Employee, Order).
* A **Value Type** represents a terminal property (e.g., FirstName, OrderDate).

#### 2.2 Fact Types
A Fact Type is a binary relation $R$ defined by a predicate $P$ over two participants:
$$R = \{(e_1, e_2) \mid P(e_1, e_2) \text{ is True}\}$$
where $e_i \in (E \cup V)$. Version 1.0 of the Ormle Standard normatively defines binary fact types (arity 2), which represent relationships expressed as natural-language readings (e.g., "Employee handles Order").

#### 2.3 Roles
Each participant in a Fact Type occupies a **Role**. A role binds an entity or value type to a specific position within the predicate and carries constraint metadata (uniqueness, mandatoriness) governing the logical behavior of the relation.

#### 2.4 Reference Schemes
A Reference Scheme defines how instances of an entity type are uniquely identified (Primary Key). Formally, for each entity type $E \in E$, the reference scheme defines an injective function:
$$ref: E \to D_{id}$$
such that $\forall a, b \in E: ref(a) = ref(b) \implies a = b$, where $D_{id}$ is the identifier domain.

---

### 3. Constraint Formalization

#### 3.1 Uniqueness Constraints and Functional Dependencies
The `isUnique` property defines a logical law. If role $r_1$ is unique in a binary relation between $E_1$ and $E_2$, we have a function $f: E_1 \to E_2$:
$$\forall x \in E_1, \forall y, z \in E_2: (P(x, y) \land P(x, z)) \implies y = z$$

#### 3.2 Mandatoriness and Existence Constraints
The `isMandatory` property defines an existence dependency. If entity $E_1$ must participate in predicate $P$:
$$\forall x \in E_1 \exists y \in E_2: P(x, y)$$
An LLM receiving this constraint knows to generate an `INNER JOIN`. Without it, the appropriate operation is a `LEFT JOIN`.

---

### 4. Schema Representation (Example)

```json
{
  "entities": [
    {
      "name": "Employee",
      "referenceScheme": "empId",
      "isValueType": false,
      "sampleValues": ["Alice Chen", "Bob Martinez"]
    },
    {
      "name": "Order",
      "referenceScheme": "orderId",
      "isValueType": false
    }
  ],
  "factTypes": [
    {
      "reading": "Employee handles Order",
      "inverseReading": "Order is handled by Employee",
      "arity": 2,
      "roles": [
        { "entityName": "Employee", "isUnique": false, "isMandatory": false },
        { "entityName": "Order", "isUnique": true, "isMandatory": true }
      ]
    }
  ]
}

[ormle.com/Standard](https://www.ormle.com/Standard)
