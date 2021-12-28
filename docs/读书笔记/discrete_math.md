# 离散数学

## Methods of Proving Theorems

If we want to prove `$q$` is true ,there are three methods:

### Direct Proofs

```math
p\land (p\to q) \text{\ is true}
```

### Proof by Contradiction

```math
\lnot q\to (\lnot r\land r)\text{\ is true}
```

### Proof by Contrposition

```math
p\land (\lnot q\to \lnot p)\text{\ is true}
```

To be honest ,this is a specific case base on **contradiction** ,which **p** is subsititude for **r** ,generally ,**p** is told in question stem ,and **r** is not.   

## Propositional logic

Proposition: A declarative sentence that is either true or false, but not both. 

Statements that can not be decided is not a proposition. 

Propositional/Statement variable: p, q, r, s 

Truth value: T, F

Propositional Calculus/Logic: The area of logic that deals with propositions. 

Compound proposition: Proposition formed from existing propositions using operators. 

Operator: 

* Not
  ¬p
  e.g. It is not the case that …

* Conjunction/And
  p ∧ q
  e.g. … and/but …

* Disjunction/Or
  p ∨ q
  e.g. … or …

* Exclusive or
  p ⊕ q

* Conditional Statement / Implication
  p → q
  * if p, then q
  * p only if q
  * p implies q
  * p is a sufficient condition for q
  * q is a necessary condition for p
  * q follows from / if / when / whenever p
  * q unless ¬p
    False only when p is true, but q is false; when p is false, p → q is defined to be true. 
  * Converse
    p → q to q → p
  * Inverse
    p → q to ¬p → ¬q
  * Contrapositive
    Converse and inverse
    p → q to ¬q → ¬p

* Biconditional statement
  p ↔ q
  * p if and only if q
  * p is necessary and sufficient for q
  * if p then q, and conversely
  * p iff q
    p ↔ q == (p → q) ∧ (q → p), only true when p and q have the same value

Operator precedence: (), ¬, ∧ ∨, →, ↔

Bit: 1 for T, 0 for F.

Bit string: a sequence of zero or more bits.

Bit operation: Bitwise AND, Bitwise OR, Bitwise XOR

## Applications of propositional logic

Translating English sentences: to logical proposition. 

Consistent system specification: no conflicting requirements; a set of value to satisfy all the statements translated; does not necessarily has a real usage.

## Propositional equivalences

Classification of compound proposition:

* Tautology
  Always true

* Contradiction
  Always false

* Contingency
  Neither a tautology nor a contradiction

Logical equivalence: Compound propositions that have the same truth values in all possible

cases: 
p ↔ q is a tautology
p ≡ q, p ⇔ q
Logical Equivalences:

| Equivalence                     | Name                |
| ------------------------------- | ------------------- |
| p ∧ T ≡ p                       | Identity laws       |
| p ∨ F ≡ p                       |                     |
| p ∨ T ≡ T                       | Domination laws     |
| p ∧ F ≡ F                       |                     |
| p ∨ p ≡ p                       | Idempotent laws     |
| p ∧ p ≡ p                       |                     |
| ¬(¬p) ≡ p                       | Double negation law |
| p ∨ q ≡ q ∨ p                   | Commutative laws    |
| p ∧ q ≡ q ∧ p                   |                     |
| (p ∨ q) ∨ r ≡ p ∨ (q ∨ r)       | Associative laws    |
| (p ∧ q) ∧ r ≡ p ∧ (q ∧ r)       |                     |
| p ∨ (q ∧ r) ≡ (p ∨ q) ∧ (p ∨ r) | Distributive laws   |
| p ∧ (q ∨ r) ≡ (p ∧ q) ∨ (p ∧ r) |                     |
| ¬(p ∧ q) ≡ ¬p ∨ ¬q              | De Morgan’s laws    |
| ¬(p ∨ q) ≡ ¬p ∧ ¬q              |                     |
| p ∨ (p ∧ q) ≡ p                 | Absorption laws     |
| p ∧ (p ∨ q) ≡ p                 |                     |
| p ∨ ¬p ≡ T                      | Negation laws       |
| p ∧ ¬p ≡ F                      |                     |
| p → q ≡ ¬p ∨ q                  |                     |
| p ↔ q ≡ (p ∧ q) ∨ (¬p ∧         |                     |
| ¬q)                             |                     |

Mine: ¬(p → q) ≡ p ∧ ¬q Mine: p ∨ (¬p ∧ q) ≡ p ∨ q See Section 3.1 No.30

Prove Logical Equivalence: Truth table or developing a series of logical equivalences.

Prove Not Logically Equivalent: (Simplify first) and find a counterexample.

Propositional Satisfiability: An assignment of truth values that makes it true.

Truth table, or whether its negation is a tautology. (or say whether itself is a contradiction?)

## Predicates and Qualifiers

Predicate: Statements involving variables, the variables are called subjects, the other is called a predicate.

The statement of P(x) is also called the value of Propositional function P at x.

Precondition: Conditions for valid input.

Postcondition: Conditions for correct output.

Qualification: Express the extent to which a predicate is true over a range of elements.

((Domain / universe) of discourse) / domain: A predicate is true for a variable in a particular domain.

Predicate calculus: The area of logic that deals with predicates and quantifiers.

Universal qualification: For every element.

∀x P(x): For all / every x P (x).

An element for which P(x) is false is called a counterexample of ∀x P(x).

Existential qualification: For one or more element.
∃x P(x): There exists an element x in the domain such that P(x).

Uniqueness qualification: ∃!x P(x) or ∃_1 x P(x)
There exists a unique x such that P (x) or There is one and only one x such that P (x).

Abbreviated qualifier notation: Use condition for domain.

Or use ∀x P(x) → Q(x) for using P(x) as condition for domain.

Quantifiers (∀ and ∃) have higher precedence than all logical operators from propositional calculus. i.e. They absorb less.

Occurrence of variable is bound: Quantifier is used on the variable.

All the variables that occur in a propositional function must be bound or set equal to a particular value to turn it into a proposition.

Scope of quantifier: The part of a logical expression to which a quantifier is applied.

The same letter is often used to represent variables bound by different quantifiers with scopes that do not overlap.

Statements involving predicates and quantifiers are logically equivalent: If and only if they have the same truth value no matter which predicates are substituted into these statements and which domain of discourse is used for the variables in these propositional functions. 

S ≡ T
∀x (P(x) ∧ Q(x)) ≡ ∀x P(x) ∧ ∀x Q(x)
∃x (P(x) ∨ Q(x)) ≡ ∃x P(x) ∨ ∃x Q(x)

De Morgan’s laws for quantifiers:
¬∀x P(x) ≡ ∃x ¬P(x)
¬∃x Q(x) ≡ ∀x ¬Q(x)

Translating from English into Logical Expression: …
Using Quantifiers in System Specifications: …

## Nested Qualifiers

Nested quantifiers: One quantifier is within the scope of another.

Understanding Statements Involving Nested

Quantifiers: …

The order of the quantifiers is important, unless all the quantifiers are universal quantifiers or all are existential quantifiers.

| Statement     | Condition for true                                    |
| ------------- | ----------------------------------------------------- |
| ∀x∀y P(x, y)  | P (x, y) is true for every pair x, y.                 |
| ∀y∀x P(x, y)  |                                                       |
| ∀x∃y P(x, y)  | For every x there is a y for which P (x, y) is true.  |
| ∃x∀y P(x, y)  | There is an x for which P (x, y) is true for every y. |
| ∃x∃y P(x, y)  | There is a pair x, y for which P (x, y) is true.      |
| ∃y∃x P (x, y) |                                                       |

Translating: …

Negation: Recursively…

## Normal forms

(Disjunctive / conjunctive) clause: Disjunctions / Conjunctions with literals (optionally negated) as its disjuncts / conjuncts.

Disjunctive / Conjunctive normal form (DNF / CNF): A disjunction / conjunction with conjunctive / disjunctive clauses as its disjuncts / conjuncts.

Full disjunctive / conjuctive normal form: Each of its variables appears exactly once in every clause. Obtained by adding ∧ (¬P(x) ∨ P(x)) to its conjuction disjuncts / ∨ (¬P(x) ∧ P(x)) to its disjunction conjuncts.

Prenex normal form: Qualifier…Predicate_without_quaulifier

## Inference

Argument: a sequence of propositions.

Premise: All but the final proposition in the argument.

Conclusion: The final proposition in the argument.

Valid argument: An argument is valid if the truth of all its premises implies that the conclusion is true.

Fallacy: Common forms of incorrect reasoning which lead to invalid arguments.

Argument form: A sequence of compound propositions involving propositional variables.

Valid argument form: An argument form is valid no matter which particular propositions are substituted for the propositional variables in its premises, the conclusion is true if the premises are all true.

The key to showing that an argument in propositional logic is valid is to show that its argument form is valid.

Using truth table to show that an argument form is valid is tedious.

Modus ponens (Mode that affirms) / the law of detachment: (p ∧ (p → q)) → q

Argument can be valid, but if any of its premise is false, its conclusion is false.

| Tautology                      | Name                   |
| ------------------------------ | ---------------------- |
| (p ∧ (p → q)) → q              | Modus ponens           |
| (¬q ∧ (p → q)) → ¬p            | Modus tollens          |
| ((p → q) ∧ (q → r)) → (p → r)  | Hypothetical syllogism |
| ((p ∨ q) ∧ ¬p) → q             | Disjunctive syllogism  |
| p → (p ∨ q)                    | Addition               |
| (p ∧ q) → p                    | Simplification         |
| ((p) ∧ (q)) → (p ∧ q)          | Conjunction            |
| ((p ∨ q) ∧ (¬p ∨ r)) → (q ∨ r) | Resolution             |

p ∧ q → (r → s) ≡ p ∧ q ∧ r → s, r is additional premise.
Resolution is commonly used: ((p ∨ q) ∧ (¬p ∨ r)) → (q ∨ r)
Also rewrite premises into separate clauses can help.
Fallacy 
Affirming the conclusion
((p → q) ∧ q) → p is not a tautology.
Denying the hypothesis
((p → q) ∧ ¬p) → ¬q is not tautology.
Begging the question (Circular reasoning)
one or more steps of a proof are based on the truth of the statement
being proved.
Rules of inference for quantified statements

| Rule of Inference                 | Name                       |
| --------------------------------- | -------------------------- |
| ∀x P(x) ∴ P(c)                    | Universal instantiation    |
| P(c) for an arbitrary c ∴ ∀x P(x) | Universal generalization   |
| ∃x P(x) ∴ P(c) for some element c | Existential instantiation  |
| P(c) for some element c ∴ ∃x P(x) | Existential generalization |

Universal modus ponens: ∀x (P(x) → Q(x)), P(a), ∴ Q(a)
Universal modus tollens: ∀x (P(x) → Q(x)), ¬Q(a), ∴ ¬P(a)

## Introduction to Proofs

Theorem / Fact / Result (定理): A statement that can be shown to be true.

Propositions: Less important theorems.

Axiom / Postulate (公理): Statements we assume to be true.

Lemma (引理): A less important theorem that is helpful in the proof of other results. (plural lemmas or lemmata)

Corollary (推论): Theorem that can be established directly from a theorem that has been proved.

Conjecture (猜想): Statement that is being proposed to be a true statement.

Direct Proof: Direct proof of a conditional statement p → q is constructed when the first step is the assumption that p is true; subsequent steps are constructed using rules of inference, with the final
step showing that q must also be true.

Indirect Proofs: Proofs that do not start with the premises and end with the conclusion.

Proof by Contraposition (证明逆否命题): We take ¬q as a premise, and using axioms, definitions, and previously proven theorems, together with rules of inference, we show that ¬p must follow.

Vacuous Proofs: If we can show that p is false, then we have a proof of the conditional statement p → q.

Trivial Proof: By showing that q is true, it follows that p → q must also be true.

Proofs by Contradiction (反证): We can prove that p is true if we can show that ¬p → (r ∧ ¬r) is true for some proposition r. i.e. r is premise and ¬r is proved if ¬p.

To rewrite a proof by contraposition of p → q as a proof by contradiction, we suppose that both p and ¬q are true. Then, we use the steps from the proof of ¬q → ¬p to show that ¬p is true.

Proofs of Equivalence: (p ↔ q) ↔ (p → q) ∧ (q → p). (if and only if)(p_1 ↔ p_2 ↔ ··· ↔ p_n) ↔ (p_1 → p_2) ∧ (p_2 → p_3) ∧ ··· ∧ (p_n → p_1).

Counterexamples: To show that a statement of the form ∀x P(x) is false, we only need to find a counterexample.

Mistakes in proofs: Division by zero, Affirming the conclusion, Denying the hypothesis, Begging the question.

## Proof Methods and Strategy

Exhaustive Proof (Proofs by exhaustion): [(p_1 ∨ p_2 ∨ · · · ∨ p_n) → q] ↔ [(p_1 → q) ∧ (p_2 → q) ∧ · · · ∧ (p_n → q)]

Eliminate cases when using exhaustive proof.

Without loss of generality (WLOG): Other cases can be proved with the same method as this case.

Exhaustive proof can be invalid if not all the cases are covered.

Existence proof: A proof of a proposition of the form ∃x P(x).

Constructive: Given by finding a witness.

Nonconstructive: Some other way, e.g. negation leads to contradiction.

Uniqueness Proof: Assert that there is exactly one element with this property. ∃x(P(x) ∧ ∀y(y = x → ¬P(y))).

Forward and backward reasoning: …

Adapting existing proofs: …

Look for counterexamples: …

Tiling: Color the board with n colors. If top-right and bottom-left square is removed, the number of squares each color is unequal, but eachdomino / polymino must cover exactly one square of each color, so tiling is impossible.

## Set

Set: A set is an unordered collection of objects. a ∈ A, a ∉ A. 

Roster method: List all the members of a set. Can use … when the general pattern is obvious. 

Set builder pattern: {x ∈ set | predicate(x)} or {x | predicate(x), x ∈ set} 

Name | Description ℕ | the set of natural numbers ℤ | the set of integers ℤ | the set of positive integers ℚ | the set of rational numbers ℝ | the set of real numbers $ℝ^+$ | the set of positive real numbers ℂ | the set of complex numbers 

Interval | Set a, b | {x | a ≤ x ≤ b} [a, b) | {x | a ≤ x < b} (a, b] | {x | a < x ≤ b} (a, b) (Open) | {x | a < x < b} 

Equal: Two sets are equal if and only if they have the same elements. ∀x(x ∈ A ↔ x ∈ B). A = B. 

The order and repetition of elements does not matter: {5, 3, 3, 1} = {1, 3, 5} 

Empty/null set: ∅ 

Singleton set: Set with a single element. 

∅ is not {∅}. 

Venn diagram: Rectangle for universal set, circle for set, dot for element.

Subset: The set A is a subset of B if and only if every element of A is also an element of B. If and only if ∀x(x ∈ A → x ∈ B). A ⊆ B.

Showing that A is a Subset of B: To show that A ⊆ B, show that if x belongs to A then x also belongs to B.

Showing that A is Not a Subset of B: To show that A $\not\subseteq$ B, find a single x ∈ A such that x ∉ B.

For every set S, ∅ ⊆ S and S ⊆ S.

Proper subset: A ⊆ B and A ≠ B. A ⊂ B.

Showing Two Sets are Equal: To show that two sets A and B are equal, show that A ⊆ B and B ⊆ A.
Size of a set: If there are exactly n distinct elements in S where n is a nonnegative integer, then S is a finite set and that n is the cardinality of S, written as |S|.

Infinite set: A set is said to be infinite if it is not finite.

Power set: Given a set S, the power set of S is the set of all subsets of the set S. $\mathcal{P}(S)$.

e.g. P(A) ∈ P(B) ⇒ P(A) ⊆ B ⇒ A ∈ B

We can reconstruct the original set from the union of all element sets in its power set. So power set uniquely identifies a set.

∅ cannot be a power set.

Ordered n-tuple: The ordered collection that has $a_1 $ as its first element, $a_2$ as its second element, … , and $a_n$ as its nth element. ($a_1$, $a_2$, … ,$a_n$).

Cartesian Product: A × B = {(a, b) | a ∈ A ∧ b ∈ B}.|A × B| = |A||B|

$A_1 × A_2 × … × A_n$ = {($a_1, a_2, … , a_n$) | $a_i ∈ A_i$ for i = 1, 2, … , n}.

Relation: A subset R of the Cartesian product A × B is called a relation.

Using Set Notation with Quantifiers: ∀x∈ S(P (x)) is shorthand for ∀x(x ∈ S → P (x)).

Truth set: The truth set of P to be the set of elements x in D for which P(x) is true.

## Set Operations

Union: The union of the sets A and B, denoted by A ∪ B, is the set that contains those elements that are either in A or in B, or in both. 

A ∪ B = {x | x ∈ A ∨ x ∈ B}.

Intersection: The intersection of the sets A and B, denoted by A ∩ B, is the set containing those elements in both A and B. 

A ∩ B = {x | x ∈ A ∧ x ∈ B}.

Disjoint: Two sets are called disjoint if their intersection is the empty set.

Difference: The difference of A and B, denoted by A − B (or A \ B), is the set containing those elements that are in A but not in B. The difference of A and B is also called the complement of B with respect to A. 

A − B = {x | x ∈ A ∧ x ∈ / B}.

Complement: Let U be the universal set. The complement of the set A, denoted by $\overline{A}$, is the complement of A with respect to U.
Therefore, the complement of the set A is U − A. A − B = A ∩ $\overline{B}$.

Set Identities:

| Identity                                         | Name                |
| ------------------------------------------------ | ------------------- |
| A ∩ U = A                                        | Identity laws       |
| A ∪∅= A                                          |                     |
| A ∪ U = U                                        | Domination laws     |
| A ∩∅=∅                                           |                     |
| A ∪ A = A                                        | Idempotent laws     |
| A ∩ A = A                                        |                     |
| $\overline{(\overline{A})} = A$                  | Complementation law |
| A ∪ B = B ∪ A                                    | Commutative laws    |
| A ∩ B = B ∩ A                                    |                     |
| A ∪ (B ∪ C) = (A ∪ B) ∪ C                        | Associative laws    |
| A ∩ (B ∩ C) = (A ∩ B) ∩ C                        |                     |
| A ∪ (B ∩ C) = (A ∪ B) ∩ (A ∪ C)                  | Distributive laws   |
| A ∩ (B ∪ C) = (A ∩ B) ∪ (A ∩ C)                  |                     |
| $\overline{A ∩ B} = \overline{A} ∪ \overline{B}$ | De Morgan’s laws    |
| $\overline{A ∪ B} = $$\overline{A}∩\overline{B}$ |                     |
| A ∪ (A ∩ B) = A                                  | Absorption laws     |
| A ∩ (A ∪ B) = A                                  |                     |
| A ∩ $\overline{A}$ =∅                            | Complement laws     |
| A ∪ $\overline{A}$ = U                           |                     |

Prove set identity: Use set builder pattern and definition.

Membership table: Set identities can also be proved using membership tables. We consider each combination of sets that an element can belong to and verify that elements in the same combinations of sets belong to both the sets in the identity. To indicate that an element is in a set, a 1 is used; to indicate that an element is not in a set, a 0 is used.

Generalized Unions and Intersections: Because unions and intersections of sets satisfy associative laws, the sets A ∪ B ∪ C and A ∩ B ∩ C are well defined.

The union of a collection of sets: The set that contains those elements that are members of at least one set in the collection. 

$$
\bigcup_{i=1}^{n}{A_i}
$$

The intersection of a collection of sets is the set that contains those elements that are members of all the sets in the collection. 

$$
\bigcap_{i=1}^{n}{A_i}
$$

Computer Representation of Sets: One of the methods is to use bit strings.

## Function

Function/Mapping/Transformation: Let A and B be nonempty sets. 

A function f from A to B is an assignment of exactly one element of B to each element of A. f : A → B. f(a) = b.

If f is a function from A to B, we say that A is the domain of f and B is the codomain of f. 

If f (a) = b, we say that b is the image of a and a is a preimage of b. The range, or image, of f is the set of all images of elements of A. Also, if f is a function from A to B, we say that f maps A to B.

Two functions are equal: When they have the same domain, have the same codomain, and map each element of their common domain to the same element in their common codomain.

Let $f_1$ and $f_2$ be functions from A to $\mathbb{R}$, then $f_1 + f_2 $ and $f_1 f_2$ are also functions from A to $\mathbb{R}$ defined for all x ∈ A by : 

$$
(f_1 + f_2)(x) = f_1(x) + f_2(x) \\
(f_1f_2)(x) = f_1(x)f_2(x)
$$

The image of S under the function f: f (S) = {t | ∃s ∈ S (t = f (s))} = {f (s)| s ∈ S}.

One-to-one/injection (单射): if and only if f (a) = f (b) implies that a = b for all a and b in the domain of f. A function is said to be injective if it is one-to-one. 

$$
\forall a\forall b(f(a) = f(b) \rightarrow a = b)
$$

Increasing if f (x) ≤ f (y), and strictly increasing: if f (x) <f (y), whenever x < y and x and y are in the domain of f.

Decreasing if f (x) ≥ f (y), and strictly decreasing if f (x) > f (y), whenever x < y and x and y are in the domain of f.

Onto/surjection (满射): if and only if for every element b ∈ B there is an element a ∈ A with f (a) = b. A function f is called surjective if it is onto.

One-to-one correspondence / bijection (双射): if it is both one-to-one and onto. We also say that such a function is bijective.

To show that f is injective: Show that if f (x) = f (y) for arbitrary x, y ∈ A with x ≠ y, then x = y.

To show that f is not injective: Find particular elements x, y ∈ A such that x ≠ y and f (x) = f (y).

To show that f is surjective: Consider an arbitrary element y ∈ B and find an element x ∈ A such that f (x) = y.

To show that f is not surjective: Find a particular y ∈ B such that f (x) ≠ y for all x ∈ A.

Inverse function: Let f be a one-to-one correspondence from the set A to the set B. The inverse function of f is the function that assigns to an element b belonging to B the unique element a in A such that f(a) = b. The inverse function of f is denoted by $f^{−1}$. Hence, $f^{−1}(b) = a$ when f(a) = b.

Composition of functions: Let g be a function from the set A to the set B and let f be a function from the set B to the set C. The composition of the functions f and g, denoted for all a ∈ A by f ◦ g, is defined by

$$
(f ◦ g)(a) = f(g(a))
$$

The graphs of functions: …
Some important functions: Floor(x): [x]

## Sequence

Sequence: A function from a subset of the set of integers (usually either the set {0, 1, 2, …} or the set {1, 2, 3, …}) to a set S. We use the notation $a_n$ to denote the image of the integer n. We call $a_n$ a term of the sequence.

Geometric progression: $a, ar, ar^2,… , ar^n$, … where a is initial term, r is common ratio.

Arithmetic progression: a, a + d, a + 2d, … , a + nd, … where a is initial term, d is common difference.

String: Finite sequence, where length is the number of terms in the string.

Empty string: λ.

Recurrence relation: An equation that expresses $a_n$ in terms of one or more of the previous terms of the sequence.

Initial condition: Specify the terms that precede the first term where the recurrence relation takes effect.

Fibonacci sequence: $f_0, f_1, f_2$,… , is defined by the initial conditions $f_0 = 0, f_1 = 1$, and the recurrence relation $f_n = f_{n−1} + f{n−2}$.

Closed formula: We say that we have solved the recurrence relation together with the initial conditions when we find an explicit formula, called a closed formula, for the terms of the sequence.

Finding closed formula: Iteration, forward substitution or backward substitution.

Lucas sequence: Fibonacci sequence with different initial condition.

Summation notation: 

$$
\sum_{i=m}^n{f(i)}
$$

where i is index of summation, m is lower limit, n is upper limit.

$$
\sum_{i=0}^n(ar^i)=\frac{ar^{n+1}-a}{r-1},r{\neq}1 \\
\sum_{i=0}^ni=\frac{n(n+1)}{2} \\
\sum_{i=0}^ni^2=\frac{n(n+1)(2n+1)}{6} \\
\sum_{i=0}^ni^3=\frac{n^2(n+1)^2}{4} \\
\sum_{i=0}^{\infty}x^i,|x|<1=\frac{1}{1-x} \\
\sum_{i=0}^{\infty}ix^{i-1},|x|<1=\frac{1}{(1-x)^2}
$$

## Cardinality of Sets

Same cardinality: If and only if there is a one-to-one correspondence from A to B. |A| = |B|

Less cardinality: If there is a one-to-one function from A to B, the cardinality of A is less than or the same as the cardinality of B. |A| ≤ |B|. When |A| ≤ |B| and A and B have different cardinality, we say that the cardinality of A is less than the cardinality of B. |A| < |B|.

Countable set: A set that is either finite or has the same cardinality as the set of positive integers is called countable.

Uncountable set: A set that is not countable is called uncountable. When an infinite set S is countable, we denote the cardinality of S by $\aleph_0$(where א is aleph). |S| = $\aleph_0$. S has cardinality “aleph null”.

Prove by showing one-to-one correspondence, or can be listed.

ℤ is countable: f(n) = n / 2, when n is even; -(n - 1) / 2, when n is odd.

$ℚ^+$ is countable: Use Cantor Diagonalization Argument for listing.

ℝ is uncountable: $0.d_i, d_i = 0$, if $d_{ii} \neq 0$; 1, if $d_{ii} = 0$ cannot be listed.

If A and B are countable sets, then A ∪ B is also countable.

Schröder-Bernstein Theorem: If A and B are sets with |A| ≤ |B| and |B| ≤ |A|, then |A| = |B|. In other words, if there are one-to-one functions f from A to B and g from B to A, then there is a one-to-one correspondence between A and B.

Can use two different functions to prove same cardinality, according to Schröder-Bernstein Theorem.

Computable / uncomputable function: If there is a computer program in some programming language that finds the values of this function. If a function is not computable we say it is uncomputable. 

Proof for existence of uncomputable function: Programs are countable (Binary can be listed), but functions are not, e.g. ℤ -> ℤ is not. 

The continuum hypothesis: (We have |$P(ℤ^+)$| = $2^{\aleph_0}$ = |ℝ| = c.) There is no cardinality such that it is greater than $\aleph_0$ and less than c, or say, c = $\aleph_1$ in sequence $\aleph_0, \aleph_1, \aleph_2$, .... 

Proving power set related cardinality: Use bit string for element sets of power set. (0, 1) and decimal representation rocks for proof. |(0, 1)| = |ℝ|, can be proved with Schröder-Bernstein Theorem.

## Counting The Basics of Counting

The product rule: Suppose that a procedure can be broken down into a sequence of two tasks. If there are $n_1$ ways to do the first task and for each of these ways of doing the first task, there are $n_2$ ways to do the second task, then there are $n_1{\cdot}n_2$ ways to do the procedure. 

The sum rule: If a task can be done either in one of $n_1$ ways or in one of $n_2$ ways, where none of the set of $n_1$ ways is the same as any of the set of $n_2$ ways, then there are $n_1 + n_2$ ways to do the task. 

The subtraction rule: If a task can be done in either $n_1$ ways or $n_2$ ways, then the number of ways to do the task is $n_1 + n_2$ minus the number of ways to do the task that are common to the two different ways. 

The division rule: There are n/d ways to do a task if it can be done using a procedure that can be carried out in n ways, and for every way w, exactly d of the n ways correspond to way w.

Counting problems can be solved using tree diagrams.

## The Pigeonhole Principle

The pigeonhole principle: If $k$ is a positive integer and $k + 1$​ or more objects are placed into $k$ boxes, then there is at least one box containing two or more of the objects.

Corollary 1: A function f from a set with k + 1 or more elements to a set with k elements is not one-to-one.

The generalized pigeonhole principle: If $N$ objects are placed into $k$​ boxes, then there is at least one box containing at least $⌈N/k⌉$ objects.

Reverse minimum: (m - 1) * k + 1

Elegant applications: …

Subsequence: Picking elements while the original order is preserved.

Theorem: Every sequence of $n^2+1$ distinct real numbers contains a subsequence of length n+1 that is either strictly increasing or strictly decreasing.

The Ramsey number R(m, n), where m and n are positive integers greater than or equal to 2, denotes the minimum number of people at a party such that there are either m mutual friends or n mutual enemies, assuming that every pair of people at the party are friends or enemies.

## Permutations and Combinations

If n is a positive integer and r is an integer with 1 ≤ r ≤ n, then there are P(n, r) = n(n − 1)(n − 2) … (n − r + 1) = n! / (n - r)! r-permutations of a set with n distinct elements.

P (n, 0) = 1

The number of r-combinations of a set with n elements, where n is a nonnegative integer and r is an integer with 0 ≤ r ≤ n, equals C(n, r) = n! / (r!(n − r)!).

Binomial coefficient: $(n, r)^T$ = C(n, r).

P (n, r) = C(n, r) · P (r, r).

C(n, r) = C(n, n − r).

A combinatorial proof of an identity is a proof that uses counting arguments to prove that both sides of the identity count the same objects but in different ways, or a proof that is based on showing that there is a bijection between the sets of objects counted by the two sides of the identity. These two types of proofs are called double counting
proofs and bijective proofs, respectively.

## Binomial Coefficient

The binomial theorem: 

$$
(x+y)^n=\sum_{j=0}^{n}\binom{n}{j}x^{n-j}y^j\\
\sum_{k=0}^{n}\binom{n}{k}=(1+1)^n=2^n\\
\sum_{k=0}^{n}(-1)^k\binom{n}{k}=(-1+1)^n=0\\
\sum_{k=0}^{n}2^k\binom{n}{k}=(2+1)^n=3^n
$$

Pascal’s identity: 

$$
\binom{n+1}{k}=\binom{n}{k-1}+\binom{n}{k}
$$

So Pascal’s triangle.

Vandermonde’s identity: 

$$
\binom{m+n}{r}=\sum_{k=0}^{r}\binom{m}{r-k}\binom{n}{k}\\
\binom{2n}{n}=\sum_{k=0}^{n}\binom{n}{n-k}\binom{n}{k}=\sum_{k=0}^{n}\binom{n}{k}^2\\
\binom{n+1}{r+1}=\sum_{j=r}^{n}\binom{j}{r}
$$

Prove by combinatorial argument: Use choosing subset, use bit string.

## Generalized Permutations and Combinations

The number of r-permutations of a set of n objects with repetition allowed is $n^r$.

There are C(n + r − 1, r) = C(n + r − 1, n − 1) r-combinations from a set with n elements when repetition of elements is allowed.

Proved by stars and bars.

Method: Stars and bars abstraction.

P426 Counting solutions to equation: Notice non-negative or positive integer, the latter implies $x_i \ge 1$.

P427 Nested loop

P427 Word letter reordering: The number of different permutations of n objects, where there are $n_1$ indistinguishable objects of type 1, $n_2$ indistinguishable objects of type 2, … , and $n_k$ indistinguishable objects of type k, is 

$$
\frac{n!}{n_1!n_2! ··· n_k!}
$$

Distinguishable objects and distinguishable boxes: The number of ways to distribute n distinguishable objects into k distinguishable boxes so that $n_i$ objects are placed into box i, i = 1, 2, … , k, equals 

$$
\frac{n!}{n_1!n_2!···n_k!}
$$

Indistinguishable objects and distinguishable boxes: The number of ways to distribute n indistinguishable objects into k distinguishable boxes so that n_i objects are placed into box i, i = 1, 2, … , k, equals the n-combination from a set with k elements when repetition is allowed, according to its proof, C(k + n - 1, n).

Distinguishable objects and indistinguishable boxes:
Can enumerate by n into m, … , but no simple closed formula.

Stirling numbers of the second kind: S(n, j) denote the number of ways to distribute n distinguishable objects into j indistinguishable boxes so that no box is empty.

Then the number of ways to distribute n distinguishable objects into k indistinguishable boxes equals$\sum_{j=1}^{k}S(n,j)$.

$$
S(n,j)=\frac{1}{j!}\sum_{i=0}{j-1}(-1)^i\binom{j}{i}(j-i)^n
$$

Indistinguishable objects and indistinguishable boxes: List partition by decreasing order.

If $p_k(n)$ is the number of partitions of n into at most k positive integers, then there are $p_k(n)$ ways to distribute n indistinguishable objects into k indistinguishable boxes.

## Generating Permutations and Combinations

Generating permutations: Lexicographic.

Next permutation: Find last pair such that $a_j < a_{j+1}$, swap minimum of $a_{j+1}, …, a_n$ that is greater than $a_j$ with $a_j$, and list remaining in increasing order.

Generating subsets: Use bit string. 

Generating r-combinations: Lexicographic. 

Next permutation of {1, 2, … , n}: Find last $a_i$ such that $a_i{\ne}$n-r+i, replace $a_i$ with $a_i+1$, $a_j$ with $a_i+j-i+1$ (increasing from $a_i+1$). (This is natural.)

## Applications of Recurrence Relations

Recurrence relation: A rule for determining subsequent terms from those that precede them.

Solution of a recurrence relation: A sequence is called a solution of a recurrence relation if its terms satisfy the recurrence relation. 

Rabbits: $f_n = f_{n-1} + f_{n-2}$.

Hanoi: $H_n=2H_{n-1}+1, H_1=1$.

Bit string without two consecutive zeros: $a_n = a_{n-1} + a_{n-2}$.

Dynamic programming.

## Solving Linear Recurrence Relations

Linear homogeneous recurrence relation of degree $k$ with constant coefficients: A recurrence relation of the form

$$
a_n=c_1a_{n-1}+c_2a_{n-2}+···+c_ka_{n-k},
$$

where $c_1, c_2, …, c_k$ are real numbers, and $c_k \neq 0$.

Characteristic equation: Suppose $a_n=r^n$, then 

$$
r^k-c_1r^{k-1}-c_2r^{k-2}-...-c_{k-1}r-c_k=0
$$

is the characteristic equation. The solutions are
called characteristic roots.

Theorem 1: Let $c_1$ and $c_2$ be real numbers. Suppose that $r^2-c_1r-c_2=0$ has two distinct roots $r_1$ and $r_2$. Then the sequence $\{a_n\}$ is a solution of the recurrence relation $a_n=c_1a_{n-1}+c_2a_{n-2}$ if and only if $a_n=α_1r_1^n+α_2r_2^n$ for $n$ = 0, 1, 2, …, where $α_1$ and $α_2$ are constants.

Theorem 2: Let $c_1$ and $c_2$ be real numbers with $c_2 \neq 0$. Suppose that $r^2-c_1r-c_2=0$ has only one root $r_0$. A sequence $\{a_n\}$ is a solution of the recurrence relation $a_n=c_1a_{n-1}+c_2a_{n-2}$ if and only if $a_n=α_1r_0^n+α_2nr_0^n$, for $n$ = 0, 1, 2, …, where $α_1$ and $α_2$ are constants.

Theorem 3: Let $c_1, c_2, ..., c_k$ be real numbers. Suppose that the characteristic equation $r^k-c_1r^{k-1}-...-c_k=0$ has $k$ distinct roots $r_1, r_2, ..., r_k$. Then a sequence $\{a_n\}$ is a solution of the recurrence relation

$$
a^n=c_1a^{n-1}+c_2a^{n-2}+...+c_ka^{n-k}
$$

if and only if 

$$
a^n = α_1r_1^n+α_2r_2^n+···+α_kr_k^n
$$

for $n$ = 0, 1, 2, …, where $α_1, α_2, ..., α_k$ are constants.

Theorem 4: Let $c_1, c_2, …, c_k$ be real numbers. Suppose that the characteristic equation 

$$
r^k - c_1r^k-1 - ··· - c_k = 0
$$

has $t$ distinct roots $r_1, r_2, …, r_t$ with multiplicities $m_1, m_2, …, m_t$, respectively, so that $m_i\geq1$ for $i$ = 1, 2, …, t and $m_1+m_2+···+m_t=k$. Then a sequence $\{a_n\}$ is a solution of the recurrence relation 

$$
a_n=c_1a_{n-1}+c_2a_{n-2}+···+c_ka_{n-k}
$$

if and only if 

$$
a_n=(α_{1, 0}+α_{1, 1}n+···+α_{1, m_1-1}n^{m_1-1})r_1^n\\
+(α_{2, 0}+α_{2, 1}n+···+α_{2, m_2-1}n^{m_2-1})r_2^n\\
+···+(α_{t, 0}+α_{t, 1}^n+···+α_{t, m_t-1}n^{m_t-1})r_t^n
$$

for $n$ = 0,
1, 2, …, where $α_{i, j}$ are constants for $1\leq{i}\leq{t}$ and $0\leq{j}\leq{m}_i-1$.

Theorem 5: If $\{a_n^{(p)}\}$ is a particular solution of the
nonhomogeneous linear recurrence relation with constant coefficients 

$$
a_n=c_1a_{n-1}+c_2a_{n-2}+...+c_ka_{n-k}+F(n),
$$

then every solution is of the form $\{a_n^{(p)}+a_n^{(h)}\}$, where $\{a_n^{(h)}\}$ is a solution of the associated homogeneous recurrence relation 

$$
a_n=c_1a_{n-1}+c_2a_{n-2}+...+c_ka_{n-k}.
$$

Theorem 6: If 

$$
F(n)=(b_tn^t+b_{t-1}n^{t-1}+...+b_1n+b_0)s^n,
$$

when $s$ is not a root of the characteristic equation of the associated linear homogeneous recurrence relation, there is a particular solution of the form 

$$
(p_tn^t+p_{t-1}n^{t-1}+...+p_1n+p_0)s^n
$$

When $s$ is a root of this characteristic equation and its multiplicity is $m$, there is a particular solution of the form 

$$
n^m(p_tn^t+p_{t-1}n^{t-1}+...+p_1n+p_0)s^n.
$$

## Generating Functions

The (ordinary) generating function for the sequence $a_0,a_1,...,a_k$,... of real numbers is the infinite series

$$
G(x)=a_0+a_1x+...+a_kx^k+...=\sum_{k=0}^\infty{a}_kx^k.
$$

We can define generating functions for finite sequences of real numbers by setting $a_{n+1}=a_{n+2}=...=0$

$f(x)=\frac{1}{1-x}$ is the generating function of $\{1\}$ for |x|<1.

$f(x)=\frac{1}{1-ax}$ is the generating function of $\{a^n\}$ for |ax|<1.

Let $f(x)=\sum_{k=0}^\infty{a}_kx^k$ and $g(x)=\sum_{k=0}^\infty{b}_kx^k$, then

$$
f(x)+g(x)=\sum_{k=0}^\infty(a_k+b_k)x^k and f(x)g(x)=\sum_{k=0}^\infty(\sum_{j=0}^ka_jb_{k-j})x^k.
$$

Let $u$ be a real number and $k$ a nonnegative integer. Then the extended binomial coefficient $\binom{u}{k}$ is defined by 

$$
\binom{u}{k}=\begin{cases}
u(u-1)...(u-k+1)/k! &\text{if } k>0\\
1 &\text{if } k=0.
\end{cases}
$$

$$
\binom{-n}{r}=(-1)^r\binom{n+r-1}{r}
$$

The extended binomial theorem: Let $x$ be a real number with |x|<1 and let $u$ be a real number. Then 

$$
(1+x)^u=\sum_{k=0}^\infty\binom{u}{k}x^k.
$$

Find number of solutions: 

$$
e_1+e_2+\cdots+e_n=C,
$$

$l_i\leq{e}_i\leq{u_i}$, then it is the coefficient of $x^C$ from $(x^{l_i}+...+x^{u_i})...(...)$. Form value $r$ with tokens of value $t_i$: When order matters, ways of exactly $n$ tokens is the coefficient of $x^r$ from $(x^{t_i}+...)^n$, so for all it is the coefficient of $x^r$ from $1+...+(x^{t_i}+...)^n$; else, it is the coefficient of
$x^r$ from $(1+...+(x^{t_i})^n)+...$.

More powerful and constraint-friendly then simple permutation and combination.

Solve recurrence relations: Multiply $x^n$ to the recurrence relation. Substitute the multiplied relation into

$$
G(x)=\sum_{k=0}^\infty{a}_kx^k=...,
$$

solve for $G(x)$, then make it a summation to see $a_n$.

Proving identity: Take combination as a coefficient of certain term.

## Inclusion-Exclusion

$$
|A\cup{B}|=|A|+|B|-|A\cap{B}|.\\
|A\cup{B}\cup{C}|=|A|+|B|+|C|-|A\cap{B}|-|B\cap{C}|-|C\cap{A}|+|A\cap{B}\cap{C}|\\
…
$$

Number of integers divisible: 

$$
\lfloor{n}/a\rfloor+\lfloor{n}/b\rfloor-\lfloor{n}/ab\rfloor.
$$

## Applications of Inclusion-Exclusion

Asking element count having none of some properties: Use inclusion-exclusion.

The number of primes (The sieve of Eratosthenes): A composite number is divisible by a prime smaller than its square root.

The number of onto functions: The shouldn’t have properties are not having element $i$ in the range.

Let $m$ and $n$ be positive integers with $m \geq{n}$. Then, there are 

$$
n^m-C(n,1)(n-1)^m+C(n,2)(n-2)^m-...+(-1)^{n-1}C(n,n-1)1^m
$$

onto functions from a set with m elements to a set with n elements.

Derangement: A permutation of objects that leaves no object in its original position.

The number of derangements of a set with $n$ elements is 

$$
D_n=n![1-\frac{1}{1!}+\frac{1}{2!}-\frac{1}{3!}+...+(-1)^n\frac{1}{n!}]\to{n}!e^{-1}.
$$

For arranging differently between two times, the number is 

$$
n!D_n=(n!)^2[1-\frac{1}{1!}+\frac{1}{2!}-\frac{1}{3!}+...+(-1)^n\frac{1}{n!}]
$$

because the first arrangement can have $n!$ ways.

## Relations, Their Properties and Representations

Binary relation: Let A and B be sets. A binary relation from A to B is a subset of $A\times{B}$. 

$a\mathrel{R}b$ or $a\not\!\!R \;b$.

Matrix representation: $M_R,m_{ij}=(a_i,b_j)\in{R}$.

Functions can be relations.

Relation on a set: A relation on a set $A$ is a relation from $A$ to $A$.

Reflexive: A relation $R$ on a set $A$ is called reflexive if $(a,a)\in{R}$ for every element $a\in{A}$.

Irreflexive: A relation $R$ on the set $A$ is irreflexive if for every $a\in{A}$, $(a,a)\not\in{R}$.

Symmetric: A relation $R$ on a set $A$ is called symmetric if $(b,a)\in{R}$ whenever $(a,b)\in{R}$, for all $a,b\in{A}$. In matrix it is 1 to 1 and 0 to 0 mirrored by the main diagonal, or $M_R=(M_R)^T$.

Asymmetric: A relation $R$ is called asymmetric if $(a,b)\in{R}$ implies that $(b,a)\not\in{R}$(So the main diagonal are all zeros).

Antisymmetric: A relation $R$ on a set $A$ such that for all $a,b\in{A}$,  if $(a,b)\in{R}$ and $(b,a)\in{R}$, then $a=b$ is called antisymmetric. In matrix it is 1 to 0, 0 to 1 or 0 to 0 mirrored by the main diagonal. Antisymmetric is not Asymmetric, but Asymmetric is Antisymmetric.

Transitive: A relation $R$ on a set $A$ is called transitive if whenever $(a,b)\in{R}$ and $(b,c)\in{R}$, then $(a,c)\in{R}$, for all $a,b,c\in{A}$. 

Combining Relations: Relations can be combined like sets.

$$
M_{R_1\cup{R}_2}=M_{R_1}\vee{M}_{R_2}\\
M_{R_1\cap{R}_2}=M_{R_1}\wedge{M}_{R_2}\\
M_{R\circ{S}}=M_S\bigodot{M}_R (\bigodot \text{stands for boolean product})\\
M_{R^n}=(M_R)^n
$$

Symmetric difference: The symmetric difference of $A$ and $B$, denoted by $A\bigoplus{B}$, is the set containing those elements in either $A$ or$ B$, but not in both $A$ and $B$.

$M_{\bigoplus R}$ is the entry-wise XORed matrix.

Composition: The composite of $R$ and $S$ is the relation consisting of ordered pairs $(a, c)$, where $a\in{A}$, $c\in{C}$, and for which there exists an element $b\in{B}$ such that $(a,b)\in{R}$ and $(b,c)\in{S}$. We denote the composite of $R$ and $S$ by $S\circ{R}$.

$S\circ{R}$ is from right to left (inside to outside)!

Composition can be done by matrix multiplication.

Power: Let $R$ be a relation on the set $A$. The powers $R^n$, $n=1, 2, 3 ,..., $ are defined recursively by $R^1=R$ and $R^{n+1}=R^n\circ{R}$.

Theorem: The relation $R$ on a set $A$ is transitive if and only if $R^n\subseteq{R}$ for $n=1, 2, 3, ...$.

Inverse relation: $R^{-1}$, with pairs inverted.

Relations on a finite set can also be represented by digraphs (directed graphs).

$$
(R\cup{S})^{-1}=R^{-1}\cup{S}^{-1}\\
(R\cap{S})^{-1}=R^{-1}\cap{S}^{-1}\\
(\overline{R})^{-1}=\overline{R^{-1}}\\
(R-S)^{-1}=R^{-1}-S^{-1}\\
(A\times{B})^{-1}=B\times{A}
$$

## Closures of Relations

Closure of $R$ with respect to **P**: The relation with property **P** containing $R$ such that it is a subset of every relation with property **P** containing $R$.

Diagonal relation: $\Delta=\{(a,a)|a\in{A}\}$.

Reflexive closure of $R$: The smallest reflexive relation that contains $R$.

Formed by $R\cup\Delta$.

Symmetric closure of $R$: The smallest symmetric relation that contains $R$.

Formed by $R\cup{R}^{-1}$.

Transitive closure of $R$: The smallest transitive relation that contains $R$.

Path: A sequence of consecutive edges, denoted by $x_0,x_1,x_2,...,x_{n-1},x_n$, with length $n$.

Circuit (or cycle): A path of length $n\geq{1}$ that begins and ends at the same vertex.

Path on relation: There is a path from $a$ to $b$ in $R$ if there is a sequence of elements $a,x_1,x_2,...,x_{n−1}$, $b$ with $(a,x_1)\in{R}$, $(x_1,x_2)\in{R}$, ..., and $(x_{n−1},b)\in{R}$.

Theorem 1: Let $R$ be a relation on a set $A$. There is a path of length $n$, where $n$ is a positive integer, from $a$ to $b$ if and only if $(a,b)\in{R}^n$.

Connectivity relation: Let $R$ be a relation on a set $A$. The connectivity relation $R^*$ consists of the pairs $(a,b)$ such that there is a path of length at least one from $a$ to $b$ in $R$.

$$
R^*=\bigcup_{n=1}^\infty{R}^n
$$

Theorem 2: The transitive closure of a relation $R$ equals the connectivity relation $R^*$.

Lemma 1: Let $A$ be a set with n elements, and let $R$ be a relation on $A$. If there is a path of length at least one in $R$ from $a$ to $b$, then there is such a path with length not exceeding $n$. Moreover, when $a\neq{b}$, if there is a path of length at least one in $R$ from $a$ to $b$, then there is such a path with length not exceeding $n−1$.

$$
R^*=\bigcup_{i=1}^nR^i
$$

Theorem 3: Let $M_R$ be the zero–one matrix of the relation $R$ on a set with $n$ elements. Then the zero–one matrix of the transitive closure $R^*$ is

$$
M_{R^*}=M_R\vee{M}_R^{[2]}\vee{M}_R^{[3]}\vee...\vee{M}_R^{[n]}.
$$

Interior vertices: Vertices of a path excluding the first and the last.

$W_0=M_R, W_i=[w_{ij}^{(k)}]$, where $w_{ij}$ is whether there is a path from $v_i$ to $v_j$ such that all interior vertices are in the first $i$ elements of the list (The list is prepared beforehand).

$$
W_n=M_{R^*}.
$$

Lemma 2: 

$$
w_{ij}^{[k]}=w_{ij}^{[k-1]}\vee(w_{ik}^{[k-1]}\wedge{w}_{kj}^{[k-1]})
$$

## Equivalence Relations

Equivalence Relation: $A$ relation on a set $A$ is called an equivalence relation if it is reflexive, symmetric, and transitive.

Equivalent: Two elements $a$ and $b$ that are related by an equivalence relation are called equivalent. The notation $a\tilde{b}$ is often used to denote that $a$ and $b$ are equivalent elements with respect to a particular equivalence relation.

Congruence Modulo $m$ is an equivalence relation.

Equivalence class: Let $R$ be an equivalence relation on a set $A$. The set of all elements that are related to an element a of $A$ is called the equivalence class of $a$. The equivalence class of $a$ with respect to $R$ is denoted by $[a]_R$. When only one relation is under consideration, we can delete the subscript $R$ and write $[a]$ for this equivalence class.

Representative of equivalence class: If $b\in[a]_R$ , then $b$ is called $a$ representative of this equivalence class.

Theorem 1: Let $R$ be an equivalence relation on a set $A$. These statements for elements $a$ and $b$ of $A$ are equivalent:

$$
aRb \\
[a]=[b] \\
[a]\cap[b]\neq\varnothing
$$

Partition: Partition of a set $S$ is a collection of disjoint nonempty subsets of $S$ that have $S$ as their union.

Theorem 2: Let $R$ be an equivalence relation on a set $S$. Then the equivalence classes of $R$ form a partition of $S$. Conversely, given a partition $\{A_i|i\in{I}\}$ of the set $S$, there is an equivalence relation $R$ that has the sets $A_i,i\in{I}$, as its equivalence classes.

The m congruence modulo classes are denoted by $[0]_m, [1]_m, ..., [m−1]_m$.

## Partial Ordering

Partial ordering: A relation $R$ on a set $S$ is called a partial ordering or partial order if it is reflexive, antisymmetric, and transitive.

Partially ordered set (poset): A set $S$ together with a partial ordering $R$ is called a partially ordered set, or poset, and is denoted by $(S,R)$. Members of $S$ are called elements of the poset.

Less/greater than or equal ($\leq/\geq$), inclusion relation ($\subseteq$), divisibility relation (|) are all partial orderings.

Less/greater than ($</>$) are antisymmetric and transitive, but not reflexive, so they are not partial orderings.

Comparable: The elements $a$ and $b$ of a poset $(S,\preceq)$ are called comparable if either $a\preceq b$ or $b\preceq a$. When $a$ and $b$ are elements of $S$ such that neither $a\preceq b$ nor $b\preceq a$, $a$ and $b$ are called incomparable.

Totally/linearly ordered set: If $(S,\preceq)$ is a poset and every two elements of $S$ are comparable, $S$ is called a totally or linearly ordered set, and $\preceq$ is called a total or linear order. A totally ordered set is also called a chain.

Well-ordered set: $(S,\preceq)$ is a well-ordered set if it is a poset such that $\preceq$ is a total ordering and every nonempty subset of $S$ has a least element.

The principle of well-ordered induction: Suppose that $S$ is a well-ordered set. Then $P(x)$ is true for all $x\in S $, if (inductive step:) For every $y\in{S}$, if $P(x)$ is true for all $x\in{S}$ with $x\prec{y}$, then $P(y)$ is true.

Lexicographic ordering: The lexical ordering $\prec$ on $A_1\times{A}_2$ is defined by specifying that one pair is less than a second pair if the first entry of the first pair is less than (in $A_1$) the first entry of the second pair, or if the first entries are equal, but the second entry of this pair is less than (in $A_2$) the second entry of the second pair.

Hasse diagram: Start with the directed graph for this relation. First, Remove these loops because of reflexivity. Next, remove all edges that must be in the partial ordering because of transitivity. Finally, arrange each edge so that its initial vertex is below its terminal vertex and remove all the arrows on edges.

Covers: An element $y\in{S}$ covers an element $x\in{S}$ if $x\prec{y}$ and there is no element $z\in{S}$ such that $x\prec{z}\prec{y}$.

Covering relation: The set of pairs $(x,y)$ such that $y$ covers $x$ is called the covering relation of $(S,\preceq)$.

Maximal element: An element of a poset is called maximal if it is not less than any element of the poset. The top element of a Hasse diagram.

Minimal element: An element of a poset is called minimal if it is not greater than any element of the poset. The bottom element of a Hasse diagram.

Greatest element: An element in a poset that is greater than every other element.

Least element: An element in a poset that is less than every other element.

Upper bound: Element greater than or equal to all the elements in a subset $A$ of $S$.

Lower bound: Element less than or equal to all the elements in a subset $A$ of $S$.

Least upper bound: Upper bound that is less than every other upper bound of a subset $A$ of $S$.

Greatest lower bound: Lower bound that is greater than every other lower bound of a subset $A$ of $S$.

Lattice: A partially ordered set in which every pair of elements has both a least upper bound and a greatest lower bound is called a lattice.

$(\mathcal{P}(S),\subseteq/\supseteq)$ is a lattice, with LUB and GLB being $A\cup{B}$ and $A\cap{B}$.

Compatible: A total ordering $\preceq$ said to be compatible with the partial ordering $R$ if $a\preceq{b}$ whenever $aRb$.

Topological sorting: Constructing a compatible total ordering from a partial ordering.

Lemma 1: Every finite nonempty poset $(S,\preceq)$ has at least one minimal element.

Algorithm for topological sorting: Pick the least element and remove it from the poset. Can also be done with a Hasse diagram.

## Graphs and Graph Models

(Undirected) graph: A *graph* $G=(V,E)$ consists of V, a nonempty set of vertices (or nodes) and E, a set of edges. Each edge has either one or two vertices associated with it, called its *endpoints*. An edge is said to *connect*, its endpoints.

Simple graph: A graph in which each edge connects two different vertices and where no two edges connect the same pair of vertices is called a simple graph.

Infinite graph: A graph with an infinite vertex set or an infinite number of edges is called an infinite graph.

Finite graph: a graph with a finite vertex set and a finite edge set is called a finite graph.

Multigraph: Graphs that may have multiple edges connecting the same vertices are called multigraphs.

Loop: Edges that connect a vertex to itself.

Pseudographs: Graphs that may include loops, and possibly multiple edges connecting the same pair of vertices or a vertex to itself.

Directed graph (digraph): A directed graph (or digraph) $(V,E)$ consists of a nonempty set of vertices V and a set of directed edges (or arcs) E. Each directed edge is associated with an ordered pair of vertices. The directed edge associated with the ordered pair $(u,v)$ is said to start at u and end at v.

Simple directed graph: A directed graph with no loops and no multiple directed edges that start and end at the same vertices.

Directed multigraphs: Directed graphs that may have multiple directed edges from a vertex to a second (possibly the same) vertex.

Multiplicity: When there are m directed edges, each associated to an ordered pair of vertices $(u,v)$, we say that $(u,v)$ is an edge of multiplicity m.

Mixed graph: A graph with both directed and undirected edges. 

## Graph Terminology and Special Types of Graphs 

Adjacent (Neighbor): Two vertices u and v in an undirected graph G are called adjacent (or neighbors) in G if u and v are endpoints of an edge e of G. Such an edge e is called incident with the vertices u and v and e is said to connect u and v.

Neighborhood: The set of all neighbors of a vertex v of $G=(V,E)$, denoted by N(v), is called the neighborhood of v. If A is a subset of V , we denote by N(A) the set of all vertices in G that are adjacent to at least one vertex in A. So, $N(A)=\bigcup_{v\in{A}}N(v)$.

Degree: The degree of a vertex in an undirected graph is the number of edges incident with it, except that a loop at a vertex contributes twice to the degree of that vertex. The degree of the vertex v is denoted by $deg(v)$.

Theorem 1, The handshaking theorem: Let $G=(V,E)$ be an undirected graph with m edges. Then 

$$
2m=\sum_{v\in{V}}deg(v).
$$

Theorem 2: An undirected graph has an even number of vertices of odd degree. Adjacent to/from, initial/terminal vertex: When $(u,v)$ is an edge of the graph $G$ with directed edges, u is said to be adjacent to v and v is said to be adjacent from u. The vertex u is called the initial vertex of $(u,v)$, and v is called the terminal or end vertex of $(u,v)$. The initial vertex and terminal vertex of a loop are the same.

In/out degree: In a graph with directed edges the in-degree of a vertex v, denoted by $deg^−(v)$, is the number of edges with v as their terminal vertex. The out-degree of v, denoted by $deg^+(v)$, is the number of edges with v as their initial vertex. (Note that a loop at a vertex contributes 1 to both the in-degree and the out-degree of this vertex.)

Theorem 3: Let $G=(V,E)$ be a graph with directed edges. Then 

$$
\sum_{v\in{V}}deg^−(v)=\sum_{v\in{V}}deg^+(v)=|E|.
$$

Underlying undirected graph: The undirected graph that results from ignoring directions of edges is called the underlying undirected graph.

Complete graph: A complete graph on n vertices, denoted by $K_n$, is a simple graph that contains exactly one edge between each pair of distinct vertices.

Noncomplete graph: A simple graph for which there is at least one pair of distinct vertex not connected by an edge.

Cycle: A cycle $C_n$, $n\geq3$, consists of $n$ vertices $v_1,v_2,...,v_n$ and edges $\{v_1,v_2\}, \{v_2,v_3\}, ..., \{v_{n−1},v_n\}, \{v_n,v_1\}$.

Wheel: We obtain a wheel W_n when we add an additional vertex to a cycle $C_n$, for $n\geq3$, and connect this new vertex to each of the $n$ vertices in $C_n$, by new edges.

n-Cube: An n-dimensional hypercube, or n-cube, denoted by $Q_n$, is a graph that has vertices representing the $2^n$ bit strings of length n.

Bipartite and bipartition: A simple graph $G$ is called bipartite if its vertex set $V$ can be partitioned into two disjoint sets $V_1$ and $V_2$ such that every edge in the graph connects a vertex in $V_1$ and a vertex in $V_2$ (so that no edge in G connects either two vertices in $V_1$ or two vertices in $V_2$). When this condition holds, we call the pair $(V_1,V_2)$ a bipartition of the vertex set $V$ of $G$.

Theorem 4: A simple graph is bipartite if and only if it is possible to assign one of two different colors to each vertex of the graph so that no two adjacent vertices are assigned the same color.

Complete Bipartite Graph: A complete bipartite graph $K_{m,n}$ is a graph that has its vertex set partitioned into two subsets of m and n vertices, respectively with an edge between two vertices if and only if one vertex is in the first subset and the other vertex is in the second subset.

Bipartite graphs can be used to model many types of applications that involve matching the elements of one set to elements of another.

Regular graph: A simple graph is called regular if every vertex of this graph has the same degree. A regular graph is called n-regular if every vertex in this graph has degree n.

Subgraph: A subgraph of a graph $G=(V,E)$ is a graph $H=(W,F)$, where $W\subseteq{V}$ and $F\subseteq{E}$. A subgraph $H$ of $G$ is a proper subgraph of $G$ if $H\neq G$.

Subgraph induced by vertex set: Let $G=(V,E)$ be a simple graph. The subgraph induced by a subset $W$ of the vertex set $V$ is the graph $(W,F)$, where the edge set $F$ contains an edge in $E$ if and only if both endpoints of this edge are in $W$.

Spanning subgraph: $H$ is a spanning subgraph of $G$ if $W=V$, $F\subseteq{E}$.

Union of graph: The union of two simple graphs $G_1=(V_1,E_1)$ and $G_2= (V_2,E_2)$ is the simple graph with vertex set $V_1\cup{V}_2$ and edge set $E_1\cup{E}_2$. The union of $G_1$ and $G_2$ is denoted by $G_1\cup{G}_2$.

## Representing Graphs and Graph

Isomorphism

Adjacency list: Vertex and Adjacent vertices for simple graph, Initial vertex and terminal vertices for directed graph.

Adjacency matrix: A (or A_G ).

Incidence matrix: 1 when edge j is incident with vertex i.

Isomorphism: The simple graphs $G_1=(V_1,E_1)$ and $G_2=(V_2,E_2)$ are isomorphic if there exists a one-to-one and onto function f from $V_1$ to $V_2$ with the property that a and b are adjacent in $G_1$ if and only if $f(a)$ and $f(b)$ are adjacent in $G_2$, for all a and b in $V_1$. Such a function f is called an isomorphism. Two simple graphs that are not isomorphic are called nonisomorphic.

Graph invariant: A property preserved by isomorphism of graphs is
called a graph invariant.

Graph invariants include: The number of vertices, the number of edges, the number of vertices of each degree (useful), bipartite, complete, wheel.

Can also check isomorphism by making a function that maps vertices and checking whether it is preserving edges using adjacent matrix.

## Connectivity

Path: A sequence of edges that begins at a vertex of a graph and travels from vertex to vertex along edges of the graph. When there are no multiple edges, the path can be denoted by its vertex sequence.

Circuit: The path is a circuit if it begins and ends at the same vertex, and has length greater than zero.

Pass through and traverse: The path or circuit is said to pass through the vertices in between or traverse the edges.

Simple A path or circuit is simple if it does not contain the same edge more than once.

Connected: An undirected graph is called connected if there is a path between every pair of distinct vertices of the graph. An undirected graph that is not connected is called disconnected.

Theorem 1: There is a simple path between every pair of distinct vertices of a connected undirected graph.

Connected component: A maximal connected subgraph of a graph. 

Cut vertex: A vertex is a cut vertex (or articulation point), if removing it and all edges incident with it results in more connected components than in the original graph.

Cut edge: If removal of an edge creates more components, the edge is called a cut edge or bridge.

Strongly connected: A directed graph is strongly connected if there is a path from a to b and from b to a whenever a and b are vertices in the graph.

Weakly connected: A directed graph is weakly connected if there is a path between every two vertices in the underlying undirected graph.

Any strongly connected directed graph is also weakly connected. Strongly connected component: A maximal strongly connected subgraph, is called a strongly connected component or strong component.

Two graphs are isomorphic only if they have simple circuits of the same length.

Two graphs are isomorphic only if they contain paths that go through vertices so that the corresponding vertices in the two graphs have the same degree.

Theorem 2: Let $G$ be a graph with adjacency matrix $A$ with respect to the ordering $v_1,v_2,...,v_n$ of the vertices of the graph (with directed or undirected edges, with multiple edges and loops allowed). The number of different paths of length $r$ from $v_i$ to $v_j$, where $r$ is a positive integer, equals the $(i,j)$th entry of $A^r$.

The graph $G$ is connected if and only if every off-diagonal entry of $A+A^2+A^3+...+A^{n−1}$ is positive. The check can end earlier if an $A^i$ is found to be so.

## Euler and Hamilton Paths

Euler circuit: A simple circuit containing every edge of graph G.

Euler path: A simple path containing every edge of graph G.

Theorem 1: A connected multigraph with at least two vertices has an Euler circuit if and only if each of its vertices has even degree.

Algorithm 1: Constructing Euler Circuits.

Theorem 2: A connected multigraph has an Euler path but not an Euler circuit if and only if it has exactly two vertices of odd degree.

Hamilton path: A simple path in a graph $G$ that passes through every vertex exactly once.

Hamilton circuit: A simple circuit in a graph $G$ that passes through every vertex exactly once.

A graph with a vertex of degree one cannot have a Hamilton circuit.

If a vertex in the graph has degree two, then both edges that are incident with this vertex must be part of any Hamilton circuit.

When a Hamilton circuit is being constructed and this circuit has passed through a vertex, then all remaining edges incident with this vertex, other than the two used in the circuit, can be removed from consideration.

A Hamilton circuit cannot contain a smaller circuit within it.

Dirac’s theorem: If $G$ is a simple graph with $n$ vertices with $n\geq3$ such that the degree of every vertex in $G$ is at least $\frac{n}2$, then $G$ has a Hamilton circuit.

Ore’s theorem: If $G$ is a simple graph with $n$ vertices with $n\geq3$ such that $deg(u)+deg(v)\geq{n}$ for every pair of nonadjacent vertices u and v in $G$, then $G$ has a Hamilton circuit.

Finding Gray code is equivalent to finding a Hamilton circuit for n-cube.

## Shortest-Path Problems

Algorithm 1: Dijkstra’s Algorithm

Theorem 1: Dijkstra’s algorithm finds the length of a shortest path between two vertices in a connected simple undirected weighted graph.

Theorem 2: Dijkstra’s algorithm uses $O(n^2)$ operations (additions and comparisons) to find the length of a shortest path between two vertices in a connected simple undirected weighted graph with n vertices.

Traveling salesperson problem: The circuit of minimum total weight in aweighted, complete, undirected graph that visits each vertex exactly once and returns to its starting point. This is equivalent to asking for a Hamilton circuit with minimum total weight in the complete graph, because each vertex is visited exactly once in the circuit.

## Planar Graphs

Planar: A graph is called planar if it can be drawn in the plane without any edges crossing (where a crossing of edges is the intersection of the lines or arcs representing them at a point other than their common endpoint). Such a drawing is called a planar representation of the graph.

Proving no planar representation: Find a loop, divide the plane into regions, divide and conquer.

$K_{3,3}$ and $K_5$ are non-planar.

Euler’s formula: Let $G$ be a connected planar simple graph with e edges and v vertices. Let r be the number of regions in a planar representation of G. Then 

$$
r=e−v+2.
$$

Proved by mathematical induction.

Corollary 1: If $G$ is a connected planar simple graph with $e$ edges and $v$ vertices, where $v\geq3$, then $e\leq3v−6$.

Can be used to show that a graph is non-planar.

Degree of a region: the number of edges on the boundary of this region.

Proved by $2e\geq3r$ and Euler’s formula.

Corollary 2: If $$$ is a connected planar simple graph, then $G$ has a vertex of degree not exceeding five.

Corollary 3: If a connected planar simple graph has e edges and v vertices with $v\geq3$ and no circuits of length three, then $e\leq2v−4$.

Proved like corollary 1, where $2e\geq4r$.

Can be used to show that a graph is non-planar.

Elementary subdivision: If a graph is planar, so will be any graph obtained by removing an edge {u,v} and adding a new vertex w together with edges $\{u,w\}$ and $\{w,v\}$. Such an operation is called an elementary subdivision.

Homeomorphic: The graphs $G_1=(V_1,E_1)$ and $G_2=(V_2,E_2)$ are called homeomorphic if they can be obtained from the same graph by a sequence of elementary subdivisions.

Kuratowski’s Theorem: A graph is nonplanar if and only if it contains a subgraph (deleting vertices and incident edges) homeomorphic to $K_{3,3}$ or $K_5$.

$K_{3,3}$ can also be a hexagon with opposing vertices connected, and the parts are the two sets of three unconnected vertices.

## Graph Coloring

Dual graph: Each map in the plane can be represented by a graph. To set up this correspondence, each region of the map is represented by a vertex. Edges connect two vertices if the regions represented by these vertices have a common border. Two regions that touch at only one point are not considered adjacent. The resulting graph is called the dual graph of the map.

Any map in the plane has a planar dual graph.

Coloring: A coloring of a simple graph is the assignment of a color to each vertex of the graph so that no two adjacent vertices are assigned the same color.

Chromatic number: The chromatic number of a graph is the least number of colors needed for a coloring of this graph, denoted by $\chi(G)$.

The four color theorem: The chromatic number of a planar graph is no greater than four.

Nonplanar graphs can have arbitrarily large chromatic numbers.

Show that the chromatic number of a graph is k:

1. Show that the graph can be colored with k colors. This can be done by constructing such a coloring.
2. Show that the graph cannot be colored using fewer than k colors, when 3 it is often shown by a three vertices loop.

The chromatic number of a complete graph $K_n$ is n because every vertex is connected with all others, and this does not contradict the four color theorem because $K_n$ is not planar when n>4.

The chromatic number of a complete bipartite graph $K_{m,n}$ is 2, by coloring either set a color.

The chromatic number of a cycle graph $C_n$, is 1 when n=1, 2 when n is even, 3 when n is odd and n>1.

Equivalent to scheduling and required number of time slots.