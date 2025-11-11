<!---
{
  "id": "0083b38f-6e8d-492c-975d-25f21e1856ec",
  "teaches": "Implementing Mathematical Mappings",
  "depends_on": ["0b6b3ce8-418e-4900-ae42-a6d068389a12"],
  "author": "Stephan Bökelmann",
  "first_used": "2025-004-03",
  "keywords": ["C Language", "math.h", "mappings"]
}
--->

# Implementing Mathematical Mappings

## 1) Introduction

The basic purpose of computing machines is to perform calculations — but not merely in the abstract sense of manipulating symbols or solving equations as in pure mathematics. Instead, we compute by **evaluating expressions** — structured combinations of values, variables, and operators that yield concrete results.

In programming, expressions are ubiquitous. They form:

- arithmetic operations like `x + y`
- function calls like `sqrt(x*x + y*y)`
- logical comparisons like `x > 0`
- assignments like `result = f(x)`

A **mapping** in mathematics defines a transformation: it takes input from a *domain* and produces output in a *codomain*. In C, we encode such mappings as **functions**, constrained by the available types.

For instance, the mathematical mapping:

```
f: ℕ₀ → ℕ₀,  f(x) = ⌊x / 2⌋ + ⌊x / 4⌋
```

can be translated to C as:

```c
unsigned int f(unsigned int x) {
    return (x / 2) + (x / 4);
}
```

Calling this function produces a deterministic result for any valid input in its domain:

```c
unsigned int result = f(10);  // evaluates to 5 + 2 = 7
```

Understanding how types like `unsigned int`, `int`, and `float` represent different mathematical sets (ℕ₀, ℤ, ℝ) is crucial when modeling computations in C.

## 2) Tasks

1. **Interpret the Signature**:\
   Given the C function:

   ```c
   unsigned int f(unsigned int x) {
       return (x / 2) + (x / 4);
   }
   ```

   - What domain and codomain does this correspond to mathematically?

2. **Implement Mathematical Mappings**:\
   Write the following functions in C:

   - **Function g**

     ```
     g(x, y) = ⌊(x + y) / 3⌋ + ⌊(x + y) / 5⌋   for x, y ∈ ℕ₀
     ```

   - **Function h**

     ```
     h(x, y, z) = √(x² + y² + z²)   for x, y, z ∈ ℤ
     ```

     Use the `sqrtf()` function from `math.h`. Make sure, to add the `-lm` flag when compiling, otherwise the Linker won't find the library!

3. \*\*Call in \*\*:\
   In your `main()` function, call the above implementations with meaningful example values and print their outputs using `printf`.

4. **Investigate the Limits**:\
   Use `printf("%u\n", UINT_MAX);` to print the largest `unsigned int` value. What happens if you try to evaluate `f(UINT_MAX)`? Does the function still behave as expected?

5. **Compose Mappings**:\
   Compute and print:

   ```c
   unsigned int a = g(6, 9);
   float distance = h(a, 3, 4);
   printf("Distance: %.2f\n", distance);
   ```

6. **Overflow Detection**:\
   Add an input check to `g` that prints a warning if `x + y` would overflow an `unsigned int`. Use:

   ```c
   if (x > UINT_MAX - y) {
       printf("Overflow!\n");
   }
   ```

## 3) Questions

1. What is the practical difference between `int`, `unsigned int`, and `float` in terms of the mathematical sets they represent?
2. What happens when a value overflows in an `unsigned int` operation?
3. Why do we use floor (⌊ ⌋) in the mathematical definition, but not explicitly in C?
4. How does the C compiler resolve the types of arithmetic expressions involving different types (e.g. `int` and `float`)?
5. Can a function in C map from a pair like `(int, float)` to a `double`? Write such a function.

## 4) Advice

Use the `-Wall -Wextra` flags when compiling with `gcc` to catch warnings. Link the math library with `-lm` if you’re using mathematical functions like `sqrt()`. Always consider the range of your input and output types — and use `limits.h` to get constants like `UINT_MAX`.

To visualize mappings, it can help to draw a simple input-output table:

| x  | f(x) |
| -- | ---- |
| 4  | 4    |
| 8  | 8    |
| 12 | 12   |
| 16 | 16   |

This reinforces the idea that **functions are mappings** and C lets us *implement* them with concrete data types.

---

Happy coding, and may your mappings never overflow!

