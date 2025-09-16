---
tags:
  - dynamicprogramming
time complexity: O(1)
---
## What is Dynamic Programming?

Dynamic programming is an **optimization technique** used to **efficiently solve problems that are computationally complex**. The key characteristic is the way dynamic programming **breaks the overall problem into smaller**, **overlapping subproblems**. Often the solutions to subproblems are stored and reused to avoid repeated work. In comparison with other approaches, this **greatly improves the efficiency of the solution**.

## A Practical Example: Determining the Nth Fibonacci Number

To quickly refresh your memory, the Fibonacci Sequence is a sequence of numbers in which every number is the sum of the two previous numbers:

```
0, 1, 1, 2, 3, 5, 8, 13, 21, …
```

We should also restate that the Fibonacci sequence is known to start with 0, 1. This represents the "base case" which will be covered in more detail later on.

Now, looking from left-to-right, it is fairly easy to see that **each number, along with its predecessor, is needed to determine the next in the sequence**. Think of this as a **“bottom-up” approach** in that it **begins with the first example and builds up to the desired solution**.

Said another way, and this time looking from right-to-left, **a given number in the sequence can be derived from the two previous numbers**. Think of this as a **"top-down" approach** in that **it begins with the desired solution and drills down toward the first example**.

Regardless of which way you look at it, the computation can be formalized as **F(n) = F(n-1) + F(n-2)**. This is known as a **recurrence relation** and is another important concept that we’ll get back to later.

Let’s now turn to some code and step through a simple top-down solution that makes use of [recursion](https://interviewing.io/recursion-interview-questions):

```typescript
function fib(n: number): number {
    if (n === 0) return 0;
    if (n === 1) return 1;
    return fib(n - 1) + fib(n - 2);
}

if (import.meta.main) {
    const k: number = 40;
  
    console.log(fib(k));
}
```

```python
def fib(n):
    if n == 0:
        return 0
    if n == 1:
        return 1
    return fib(n - 1) + fib(n - 2)
```

Consider what happens when invoked as `fib(5)` to determine the fourth Fibonacci number.

`N - 1 = 4` and `N - 2 = 3` so this function makes recursive calls to `return fib(4) + fib(3)`. Notice that the invocation of `fib(4)` will in turn make recursive calls `fib(3)` and `fib(2)`. This highlights the overlapping subproblems and where work is being repeated. The function calls can also be represented as a tree to visualize and identify the repeated work:

![An image showing the repeated work when solving nth Fibonacci recursively.](https://strapi-iio.s3.us-west-2.amazonaws.com/dynamic_programming_fibonnaci_repeated_work_30ff271031.png?updated_at=2023-06-30T15:57:14.215Z)

In the end, solving for the fifth Fibonacci number ends up solving for:

- The fourth Fibonacci number once
- The third number twice
- The second number three times
- The first number five times

This is where dynamic programming really shines as it helps avoid repeating work and provides a far more efficient solution.

#### Incorporating Memoization to Avoid Repeated Work

In the recursive algorithm for this problem the answer to `fib(3)` (and all other subproblems) is immediately discarded; what a waste!

Instead, we can **utilize a hashmap to store the return value of `fib(3)`** and later when the same subproblem comes up, **the result can be quickly retrieved**, with **O(1) time complexity**, instead of repeating it all over. Summing two numbers a handful of times for low values of N may not seem like a big deal, but as N gets subproblem repetition increases rapidly. This technique of caching the result of a function call, in order to avoid making the same call again in future, is known as [memoization](https://interviewing.io/memoization-interview-questions).

```typescript
function topDownFib(n: number): number {
    const dp: number[] = new Array(n + 1).fill(0);
    return topDownFibHelper(n, dp);
}
  
function topDownFibHelper(n: number, dp: number[]): number {
    if (n === 0 || n === 1) {
        return n;
    }
    // If value is not set in cache, compute it
    if (dp[n] === 0) {
        dp[n] = topDownFibHelper(n - 1, dp) + topDownFibHelper(n - 2, dp);
    }
    return dp[n];
}
  
if (import.meta.main) {
    const k: number = 100;

    console.log(topDownFib(k));
}
```

```python
def topDownFib(n):
    dp = [0] * (n+1)
    return topDownFibHelper(n, dp)

def topDownFibHelper(n, dp):
    if n == 0 or n == 1:
        return n
    # If value is not set in cache, compute it
    if dp[n] == 0:
        dp[n] = topDownFibHelper(n-1, dp) + topDownFibHelper(n-2, dp)
    return dp[n]
```

#### Working Iteratively from the Bottom Up Using Tabulation

Similarly, this problem can be solved from the bottom up, calculating and storing each number in the sequence along the way. This style of storing and reusing results is known as “**tabulation**”.

```typescript
function bottomUpFib(n: number): number {
    if (n === 0) return 0;
    // Initialize cache

    const dp: number[] = new Array(n + 1).fill(0);
    dp[1] = 1;

    // Fill cache iteratively
    for (let i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[n];
}
  
if (import.meta.main) {
    const k: number = 100;

    console.log(bottomUpFib(k))
}
```

```python
def bottomUpFib(n):
    if n == 0:
        return 0
    # Initialize cache
    dp = [0] * (n+1)
    dp[1] = 1
 
    # Fill cache iteratively
    for i in range(2, n+1):
        dp[i] = dp[i-1] + dp[i-2]
    
    return dp[n]
```

Although an array can be used for tabulation when solving for Fibonacci (and in fact is excessive since at most 2 previous previous results are ever needed), it demonstrates a concept that often **needs to be extended as far as using multi-dimensional arrays** to solve more **complex problems**.

#### A Quick Recap on What We Learned via Fibonacci

After considering Fibonacci from different perspectives and seeing two contrasting approaches, we’ve now been introduced to all the core concepts associated with dynamic programming:

1. **Base cases** and the **sub-problems** that give light to a **recurrence relation**
2. **Top-down approaches** which typically involve **recursion** and **memoization**
3. **Bottom-up approaches** that are usually **iterative** and use **tabulation**

Let’s move on to look at when and how to apply Dynamic programming in interviews.

## Using Dynamic Programming in Interviews

Before getting to the more formal concepts that determine whether dynamic programming can be applied, let's look at some basic heuristics to use in an interview to determine whether to even consider dynamic programming.

### Heuristics for Identifying Dynamic Programming Problems

The first [[Heuristic]] comes from considering the problem statement. Does it ask for the **min/max out of a set of possible options**, the **best/worst of a set of possible options**, or **perhaps the total number of options**? This isn't confirmation that dynamic programming is suitable, or even that's the best approach, but it is a **good signal that DP is worth exploring**.

As always in a technical interview, it's good practice to **discuss and work through one or two simple-ish examples**. Doing so helps to clarify the interviewer's requirements and expectations, plus it provides test cases for later. While working through the examples you likely identified a brute-force approach. And in **explaining how the brute force work leads to the result**, did you find yourself mentioning that the more complex example "**follows on from**" or "**makes use of**" the simpler example? This is a second [[Heuristic]] and it's a great **indication that there are sub-problems** and **repeated work** which **means a dynamic programming approach could work well**.

Does a **programmatic solution involving recursion become apparent**? **Where does the recursion lead**? **Eventually it must "bottom out"** and this is **likely to be the base case**. What are the **branches** or **conditional paths** that **trigger recursive** calls? They will likely form **part of the recurrence relation**. The availability of a recursive solution is a third [[Heuristic]] you can look for.

With one or more of these [[Heuristic]]s present, you can be confident spending time and looking hard for a dynamic programming solution.

### Optimal Substructure and Overlapping Subproblems

More formally, in order **to apply dynamic programming to a problem two conditions must be present**:

1. Optimal substructure
2. Overlapping subproblems

#### Optimal Substructure

Optimal substructure **requires that you can solve a problem based on the solutions of subproblems**. For example, if you want to calculate the 5th Fibonacci number, it can be solved by computing fib(5) = fib(4) + fib(3). It is **not necessary to know any more information other than the solutions of those two subproblems** in order to determine the solution.

A useful way to think about optimal substructure is **whether a problem can be easily solved recursively**. Recursive solutions **inherently solve a problem by breaking it down into smaller subproblems**. If you can solve a problem recursively, it **most likely has an optimal substructure**.

#### Overlapping Subproblems

Overlapping subproblems means that when you split your problem into subproblems, you sometimes get the same subproblem multiple times. With the Fibonacci example, if we want to compute `fib(5)`, we need to compute `fib(4)` and `fib(3)`. However, to compute `fib(4)`, we need to compute `fib(3)` again. This is a wasted effort, since we’ve already computed the value of `fib(3)`.

Dynamic programming **relies on overlapping subproblems**, and it **uses memory to save the values that have already been computed** to avoid computing them again. The **more overlap there is**, the **more computational time is saved**.

### The FAST Method

**FAST** is an acronym that stands for **F**ind the first solution, **A**nalyze the solution, identify the **S**ubproblems, and **T**urn around the solution.

It isn’t the only way to work through problems to reach a dynamic programming solution, but **aims to be easy to remember** and apply while being broadly applicable.

Let’s break down each of these steps.

#### Find the First Solution

The first step to solving any dynamic programming problem using The FAST Method is to **find an initial brute force recursive solution**. Solve the problem without concern for efficiency, just as a starting point. Though there are a couple of constraints on how this brute force solution should look:

- **Recursive functions should be self-contained.** Storing results by updating global variables may make it impossible to introduce memoization later on. **Craft a function** that is **solely dependent on its parameters** and **not affected by outside** factors.
    
- **Avoid unnecessary recursive function arguments.** Subproblem results will eventually be memorized based on the arguments; **the fewer the better**.
    

#### Analyze the First Solution

Analyze the initial brute force solution. This involves determining the time and space complexity and **determining if there are any obvious areas for improvement**.

As part of the analytical process, confirm that the first solution fits the rules for problems with Dynamic programming solutions:

- Does it have an **optimal substructure**?
- Are there **overlapping subproblems**?

#### Subproblem Identification

If there is indeed a Dynamic programming solution, the **appropriate subproblems can now be identified and coded**. Apply memoization to avoid unnecessary repeated work. At this point the **problem is solved with a top-down solution** that likely **exhibits optimal complexity** and no **does not repeat any work**.

#### Turn the Solution Around

Since we understand the problem well, we can go further. This involves **coding the alternate bottom-up approach** that **iteratively computes** and **uses tabulation to store the results** of successive subproblems, until the overall solution is reached. Turning the solution to **bottom-up is generally** desired as it **avoids** **pitfalls associated with recursion** and **the call stack**.

### Deciding on Top-down/Memoization vs. Bottom-up/Tabulation

In an interview, the choice of top-down or bottom-up approaches should be balanced with **other factors beyond performance**: **How easily can the bottom-up solution be coded**, **is it as easily reasoned about** and **discussed with the interviewer**? Which **approach** are you **most comfortable with**? That may be the most important factor of all!

## Common Mistakes in Interviews Featuring Dynamic Programming

1. **Jumping too quickly to conclude dynamic programming is necessary**. When you **have a hammer**, **everything** starts to **look like a nail**. If the problem doesn’t require an optimal solution but rather any correct solution, a **greedy approach will likely be simpler** to identify and implement.
    
2. **Conversely, looking too hard for a greedy solution and failing to recognize a dynamic programming problem.** A way to determine which solution is more appropriate is **to know whether a sub-solution helps lead to the final solution**. **If a sub-solution (a solution with a part of the input) helps**, then **dynamic programming is probably the way to go**!
    
3. **Failing to identify how to break the problem into subproblems so that the recurrence relation and base case(s) become clear.** When you have a strong intuition (or have been told) that a problem needs a Dynamic programming solution, this is the major challenge. Reviewing plenty of questions and gaining practice is essential.
    
4. **Struggling to define and work with a suitable result matrix.** Many problems (such as Longest Common Subsequence) involve two- or multi-dimensional arrays to store sub-problem results. These can be difficult to conceive and may be tricky to work with in code. Again it’s all about **practice**.
    

![Diagramming a multi-dimenisional array used for tabulation.](https://strapi-iio.s3.us-west-2.amazonaws.com/dynamic_programming_tabulation_5ca70457ee.png?updated_at=2023-06-30T15:59:29.606Z)

5. **Lack of clarity in communicating** your dynamic programming logic. **Visualizations can help a great deal here**. As we’ve seen in this article, **sketching a recursive tree** or a **matrix table** can be **helpful tools to gain shared understanding** with your interviewer.

## What to Say in Interviews to Show Mastery Over Dynamic Programming

- **Articulate why dynamic programming is applicable** (overlapping subproblems and optimal substructure) **for a given problem**.
- **Refer to the recurrence relation** and base case(s). **Reason about** and **justify** that the **subproblem dependencies are acyclic**.
- Discuss and ask the interviewer if they have a **preference when it comes to the tradeoffs** between **top-down** (recursive) and **bottom-up** approaches.