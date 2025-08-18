# If an algorithm takes T(N) = 5N^3 + 2N^2 + 100 operations for an input size N, what is its asymptotic Big O notation? Explain. (Conceptual, in comments).

```c

/*

If an algorithm takes T(N) = 5N^3 + 2N^2 + 100 operations for an input size N,
what is its asymptotic Big O notation? Explain. (Conceptual)

Answer:

Big O: O(N^3)

Explanation:

1) Dominant Term:
   - As N grows large, the highest-order term dominates the growth of T(N).
   - In T(N) = 5N^3 + 2N^2 + 100, the dominant term is 5N^3.

2) Ignore Constants:
   - Big O ignores constant multipliers because they do not affect growth rate classification.
   - 5N^3 → N^3 (constant factor 5 is dropped).

3) Ignore Lower-Order Terms:
   - Lower-order terms (2N^2, 100) become insignificant compared to N^3 as N → ∞.

Therefore:

T(N) ∈ O(N^3).

(Notes)
- More precise: T(N) is also Θ(N^3) because N^3 both upper- and lower-bounds T(N) up to constants.
- Practical meaning: runtime grows roughly proportional to the cube of input size for large N.
*/


```
