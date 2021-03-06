# Finitism
A minimalistic logic-free calculus for meta-reasoning.

## Introduction
The main purpose of our system is to establish termination of certain syntactic algorithms (in particular, cut elimination/normalization for various deductive systems and construction calculi) relative to respective induction principles.

We seek our system to be able to represent both algorithms defined in the language of a suitable flavour of Intuitionistic Dependent Type Theory and induction principles (constructive ordinals) used as their computability witnesses in a straightforward and transparent manner, while being much weaker than Primitive Recursive Arithmetic, ideally too weak to employ the Diagonal Argument to observe its own incompleteness (i.e. weaker than Rudimentary Function Arithmetic).

Recently developed flavours of Intuitionistic Dependent Type Theory (we consider the name "Calculus of Constructions" more enlightening) provide neccessary expressivity for representing formal languages for any sensible mathematical theory in faithful and obviously correct-by-construction way in terms of pure inductive data types[[1](http://gallais.github.io/pdf/draft_fscd17.pdf),[2](http://gallais.github.io/pdf/cpp2017.pdf),[3](http://www.cs.nott.ac.uk/~psztxa/publ/tt-in-tt.pdf)]. Pure inductive data types can be mechanically mapped to natural numbers one-to-one, so termination of a syntactic algorithm is a semi-decidable arithmetical predicate dependent on a single natural number. The semi-decidability means that if it does terminate for a given argument `n`, one can be assured of it in a finite number of steps of finite total duration and finite demand for (discrete) memory.

So, the judgements we want to be able to prove should have the form `A ⊢ B`, where both `A` and `B` are composable\* semidecidable arithmetical predicates dependent on the same parameter `n` taking values in natural numbers, `B(n)` represents termination of certain algorithm on input `n`, while `A(n)` guarantees the availability of enough computational resources for `B(n)` to be carried out.  
The judgement
```
A ⊢ B
```
is then to be read as  
"whenever `A(n)` (can be shown to hold / terminate / be solvable), also `B(n)` (can be shown to hold / terminate / be solvable)".

Without loss of generality (due to [MRDP-Theorem](https://en.wikipedia.org/wiki/Hilbert%27s_tenth_problem)) we may assume such predicates to be represented as systems of polynomial equations with one or more natural number-valued variables ("Diophantine equations"). We will stick to that representation and sometimes call `A` the "solvability witness" of `B`. We do not want however to exclude other possible representations of the predicates, especially we don't want to preclude possible natural game semantics of our system.


## Diophantine Representation of Predicates
Let our sequents be sets of equations with one parameter `x` and one or more variables. The intended domain of the variables and parameter are natural numbers (including zero). Allowed operations are `n + m` (addition), `n'` (increment), `n*` (`n`-th triagonal number). With triagonal operation, both multiplication and Cantor pairing function can be defined:
```
ab + a* + b* = (a + b)*
pair = (a + b)* + b
```

Representations are understood up to renaming.

## Operations and Rules
First of all, let us introduce the Id-rule for any sequent `A`:
```
––––———
 A ⊢ A
```

Let us define following operations on expressions:

Direct Join
: Whenever we have two predicates `A` and `B` with disjoint variables, we may construct predicate `A, B` by adjoining the equations of `A` and `B`. If the variables are not disjoint, join operation renames them suitable.

```
 A ⊢ X     B ⊢ Y
––––———–––––––––—
   A, B ⊢ X, Y
```

Composition
: Given expressions `A` and `B` with mutually disjoint sets of variables, and `b` a variable from `B` let `A ∘ b/B` denote the system of equations generated by subsitituting `b` as parameter (`x`) into the system `A` while adjoining equations from the system `B`. If variables of `A` and `B` are not disjoint, variables of `B` are renamed suitably.

```
   A ⊢ B     X ⊢ Y
——————————————————————
 A, X ∘ n/B ⊢ Y ∘ n/B 
```

Bounded Quantification
: Given an expression `A`, let `A*` denote a system of equations solvable for parameter `x = (q + p)* + p` iff A is solvable for each `x = (q + z)* + z` where z < p.

```
TODO: Rule for bounded quantification
```

Iteration
: Given an expression `A` with variable `a` we define `(a/A)'` to be an expression taking a pair `x = (n + m) + m`, then composing `A` with itself `n` times over variable `a` and feeding `m` into it as a parameter.

```
          X ⊢ Y
————————————————————————––
 (X ∘ n/(n/Y)')* ⊢ (n/Y)'
```

## Representation of Induction and Recursion
