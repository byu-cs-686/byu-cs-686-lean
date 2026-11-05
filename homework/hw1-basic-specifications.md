# Homework 1: Specifications and Proofs in Lean

This homework introduces writing specifications and proving properties of simple functions in Lean. You will write ordinary definitions for the mathematical properties and computational functions, then state the desired relationships as theorems and prove them. Lean checks the proofs; the functions can also be evaluated. For the arithmetic problems, use Lean's unbounded `Int` and `Nat` types, which have no overflow or wrapping to worry about.

Read the relevant sections of [Functional Programming in Lean](https://lean-lang.org/functional_programming_in_lean/):

- [1.2. Types](https://lean-lang.org/functional_programming_in_lean/Getting-to-Know-Lean/Types/)
- [1.3. Functions and Definitions](https://lean-lang.org/functional_programming_in_lean/Getting-to-Know-Lean/Functions-and-Definitions/)
- [Interlude: Propositions, Proofs, and Indexing](https://lean-lang.org/functional_programming_in_lean/Interlude___-Propositions___-Proofs___-and-Indexing/), especially its [Tactics section](https://lean-lang.org/functional_programming_in_lean/Interlude___-Propositions___-Proofs___-and-Indexing/#tactics)

The interlude introduces propositions and proofs, which provide the Lean counterpart to writing and verifying specifications. In Lean, a theorem's hypotheses serve as preconditions and its conclusion serves as a postcondition. Its Tactics section introduces tactic proofs and discusses `decide` and `simp`. For additional tactics used in these problems, including `by_cases`, `constructor`, `exact`, `rw`, and the arithmetic tactic `omega`, consult the [Lean 4 Language Reference: Tactic Proofs](https://lean-lang.org/doc/reference/latest/Tactic-Proofs/) and its [Tactic Reference](https://lean-lang.org/doc/reference/latest/Tactic-Proofs/Tactic-Reference/). The book's introduction is enough to get started; use the reference as needed.

## Problems

For every problem, state the mathematical property first, then define the function, then prove a theorem connecting the two, including all assumptions the conclusion needs. Small `example` declarations check concrete cases but do not replace the general theorems.

1. **Values in a stepped range.** Given a value, a range `[min, max]`, and a positive step, determine whether the value is reached by starting at `min` and repeatedly adding `step`, without exceeding `max`.

   - Define a proposition describing when an `Int` value is in the stepped range. State explicitly that the step is positive and the value lies between the endpoints.
   - Define a Boolean function that computes the answer.
   - Prove a correctness theorem relating the Boolean result to the proposition.
   - Include checked examples for boundary values, values that are not on the step sequence, a value outside the range, and a non-positive step.

   Treat all integer arguments as mathematical integers; do not model fixed-width overflow.

   **Suggested approach:** Make the specification a proposition containing the positive-step, bounds, and divisibility conditions. Define the Boolean result by testing those conditions. For the correctness theorem, unfold the definitions, split the Boolean conjunctions and the `↔` into their parts, and relate each `decide` test to its proposition.

1. **Absolute difference.** Given two `Int` values, define their absolute difference as a `Nat`.

   - Define a mathematical specification for the absolute difference.
   - Prove that the specification is commutative.
   - Define a computational function for the absolute difference using an approach different from the specification.
   - Prove that the computational function agrees with the specification.
   - Include checked examples, including inputs on opposite sides of zero.

   The point is to prove that two independently written definitions agree.

   **Suggested approach:** Prove commutativity by considering the two possible orders of the inputs. In each case, use the order facts to simplify the subtraction and absolute value. For correctness, use the same cases to show the chosen nonnegative difference has matching `toNat` and `natAbs` values. `omega` can derive the needed linear integer inequalities and subtraction equalities.

1. **Median of five.** Define a function that computes the median of three `Int` values. Use it to define a median-of-medians filter for five values by taking the medians of the overlapping triples `(a, b, c)`, `(b, c, d)`, and `(c, d, e)`, and then taking the median of those three results.

   Prove that when `a ≤ b ≤ c ≤ d ≤ e`, the filter returns `c`, the median of the five values. State the sortedness conditions as theorem hypotheses.

   **Suggested approach:** First prove a helper theorem for `median3` when its inputs are already sorted. Then unfold the five-value filter and use that helper on each of its three overlapping triples and once more on the resulting triple of medians.

## What to submit

Submit one Lean source file named `hw1.lean` containing the definitions, theorems, proofs, and checked examples for all three problems. Label each problem clearly in the file.
