# Knowledge - CS50AI Lecture 1

#### Knowledge-based agents:

Agents that reason by operating on internal representations of knowledge.

#### Sentence:

An assertion about the world in a knowledge representation language

## Propositional Logic

A type of logic that supports joining and/or modifying entire propositions, statements, or sentences to reach conclusions.

### Propositional Symbols:

_P_, _Q_, _R_

### Logical Connectives:

¬ (not)   
∧ (and)  
∨ (or)  
→ (implication)  
↔ (biconditional)

#### Not (¬)

| _P_   | ¬*P*  |
| ----- | ----- |
| false | true  |
| true  | false |

#### And (∧)

| _P_   | _Q_   | _P_ ∧ _Q_ |
| ----- | ----- | --------- |
| false | false | false     |
| false | true  | false     |
| true  | false | false     |
| true  | true  | true      |

#### Or (∨)

| _P_   | _Q_   | _P_ ∨ _Q_ |
| ----- | ----- | --------- |
| false | false | false     |
| false | true  | true      |
| true  | false | true      |
| true  | true  | true      |

#### Implication (→)

| _P_   | _Q_   | _P_ → _Q_ |
| ----- | ----- | --------- |
| false | false | true      |
| false | true  | true      |
| true  | false | false     |
| true  | true  | true      |

Ex: Your uncle says, <br> 
"_If you get a good grade, I will buy you ice cream_" <br>
_You did not get a good grade_, but your uncle was nice and still got you ice cream. <br>
_You did not get a good grade_, your uncle kept his word and didn't get you ice cream.

Conclusion: If _P_ is false, then _Q_ can be anything.

#### Biconditional (↔)

| _P_   | _Q_   | _P_ ↔ _Q_ |
| ----- | ----- | --------- |
| false | false | true      |
| false | true  | false     |
| true  | false | false     |
| true  | true  | true      |

Equivalent to:
_P_ → _Q_ ∧ _Q_ → _P_

#### Model:

Assignment of a truth value to every propositional symbol (a "possible world").

#### Knowledge base:

A set of sentences known by a knowledge-based agent.

#### Entailment:

_α_ ⊨ _β_

In every model in which sentence **α** is true, sentence **β** is also true.

#### Inference:

The process of deriving new sentences from old ones.

Ex:

**_P_** : It is a Tuesday.  
**_Q_** : It is raining.  
**_R_** : Harry will go for a run.

**_KB_**: (**_P_** ∧ ¬**_Q_**) → **_R_**

Inference: **_R_**

### Model Checking:

- To determine if **KB** entails _α_:
  - Enumerate all possible models.
  - If in every model where **KB** is true, _α_ is true, then **KB** entails _α_
  - Otherwise, **KB** does not entail _α_

**_P_** : It is a Tuesday **_Q_** : It is raining. **_R_** : Harry will go for a run.

**Knowledge Base**: (**_P_** ∧ ¬ **_Q_**) → **_R_**

**_P_** is true.  
**_Q_** is true.

Query: **_R_**

| **_P_** | **_Q_** | **_R_** | **_KB_** |
| ------- | ------- | ------- | -------- |
| false   | false   | false   | false    |
| false   | false   | true    | false    |
| false   | true    | false   | false    |
| false   | true    | true    | false    |
| true    | false   | false   | false    |
| **true**|**false**| **true**| **true** |
| true    | true    | false   | false    |
| true    | true    | true    | false    |

## Inference Rules

If there is ever an empty clause after applying these rules, it evaluates to false.
Ex: P ∧ ¬P leads to a contradiction ∴ false.

### Modus Ponens

```
α → β
  α
―――――
  β
```

Ex:

If it is raining, then Harry is inside (α → β).  
It is raining (α).  
Harry is inside (β).

### And Elimination

If both α and β are true, then one of them must also be true.

```
α ∧ β
―――――
  α
```

Ex:

Harry is friends with Ron and Hermione (α ∧ β).  
Harry is friends with Hermione (β).

### Double Negation Elimination

If the premise is `not(not(α))`, then the conclusion is α.

```
¬(¬α)
―――――
  α
```

Ex:

It is not true that Harry did not pass the test (¬(¬α)).  
Harry passed the test (α).

### Implication Elimination

If α implies β, then either not α or β is true.

```
 α → β
―――――――
¬α ∨ β
```

Ex:

If it is raining, then Harry is inside (α → β).
It is not raining or Harry is inside (¬α ∨ β).

### Biconditional Elimination

α is true if and only if β is true, in which case α implies β and β implies α.

```
        α ↔ β
―――――――――――――――――――――
  (α → β) ∧ (β → α)
```

Ex:

It is raining if and only if Harry is inside (α ↔ β).  
If it is raining, then Harry is inside, and if Harry is inside, then it is raining ((α → β) ∧ (β → α)).

### De Morgan's Law

If it is not true that α and β, then either not α or not β.

```
  ¬(α ∧ β)        Inverse:  ¬(α ∨ β)
―――――――――――――             ―――――――――――――
   ¬α ∨ ¬β                   ¬α ∧ ¬β
```

Example:

It is not true that both Harry and Ron passed the test (¬(α ∧ β)).  
Harry did not pass the test or Ron did not pass the test (¬α ∨ ¬β).

### Distributive Property

```
    (α ∧ (β ∨ γ))
―――――――――――――――――――――
  (α ∧ β) ∨ (α ∧ γ)
```
and
```
    (α ∨ (β ∧ γ))
 ―――――――――――――――――――――
  (α ∨ β) ∧ (α ∨ γ)
```

Example:

Ron is in the Great Hall or Hermione is in the library (P ∨ Q).  
Ron is not in the Great Hall (¬P).  
Conclusion: Hermione is in the library.

Ron is in the Great Hall or Hermione is in the library (P ∨ Q).  
Ron is not in the Great Hall or Harry is sleeping (¬P ∨ R).  
Conclusion: Hermione is in the library or Harry is sleeping (Q ∨ R).

#### Proving Theorems:

- Initial state: starting knowledge base.
- Actions: inference rules.
- Transition model: new knowledge base after inference.
- Goal test: check statement we're trying to prove.
- Path cost function: number of steps in proof.

### Conjuctive Normal Form:

A logical sentence that is an accumulation of individual clauses using the `∧` connective.  
Any sentence can be turned into CNF by applying inference rules.

Example:

(_A_ ∨ _B_ ∨ _C_) ∧ (_D_ ∨ _¬E_) ∧ (_F_ ∨ _G_)

### Inference by Resolution

#### Factoring:

When there are duplicate variables, we can eliminate them without affecting the meaning of the sentence.

Ex:

```
   P ∨ Q ∨ S
  ¬P ∨ R ∨ S
――――――――――――――
  (Q ∨ S ∨ R)
```

### Algorithm

To determine if **_KB_** ⊨ _α_:

- Check if (**_KB_** ∧ ¬*α*) is a contradiction?
  - If so, then **_KB_** ⊨ _α_.
  - Otherwise, no entailment.

To determine if **_KB_** ⊨ _α_:

- Convert (**_KB_** ∧ ¬*α*) to Conjunctive Normal Form.
- Keep checking to see if we can use resolution to
  produce a new clause.
  - If ever we produce the empty clause (equivalent
    to False), we have a contradiction and **_KB_** ⊨ _α_.
  - Otherwise, if we can't add new clauses, there is no
    entailment.

Example:

Does (A ∨ B) ∧ (¬B ∨ C) ∧ (¬C) entail A?

```
(A ∨ B) ∧ (¬B ∨ C) ∧ (¬C) ∧ (¬A)
```
then,
```
(¬B ∨ C) - (¬C) → (¬B)
```
then,
```
(A ∨ B) - (¬B) → (A)
```
then,
```
(¬A) - (A)
```
then,
```
()
```

When `¬A` is true there is a contradiction ∴ `¬A` has to be false meaning `A` is true and (A ∨ B) ∧ (¬B ∨ C) ∧ (¬C) entails A.