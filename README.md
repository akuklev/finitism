# Finitism
An extremely weak logic-free calculus for meta-reasoning.

## Expressions and Operations on Them
Expressions are sets of equations with one parameter `x` and one or more variables. The intended domain of the variables and parameter are natural numbers (including zero). Allowed operations are `n + m` (addition), `n'` (increment), `n*` (`n`-th triagonal number). With triagonal operation, Cantor pairing function can be defined directly:
```
pair = (a + b)* + b
```

We define following operations on expressions:
Composition
: Given expressions `A` and `B` with mutually disjoint sets of variables, and `b` a variable from `B` let `A ∘ b/B` denote the system of equations generated by subsitituting `b` as parameter (`x`) into the system `A` while adjoining equations from the system `B`. If variables of `A` and `B` are not disjoint, variables of `B` are renamed suitably.

Iteration
: Given an expression `A` with variable `a` we define `(a/A)'` to be an expression taking a pair `x = (n + m) + m`, then composing `A` with itself `n` times over variable `a` and feeding `m` into it as a parameter.

Bounded Quantification
: Given an expression `A`, let `A*` denote a system of equations solvable for parameter `x = (q + p)* + p` iff A is solvable for each `x = (q + z)* + z` where z < p.
