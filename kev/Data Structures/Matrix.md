---
tags:
  - matrix
  - datastructure
---

## What is a Matrix?

Most of us already have familiarity with matrices, but for completeness, let's go through a brief introduction. A matrix is simply a **two-dimensional grid of values** (like a bunch of **stacked cubbies**). In mathematics, an n by m matrix would be represented as follows:

![A Mathematical Representation of a Matrix](https://strapi-iio.s3.us-west-2.amazonaws.com/matrix_mathematical_representation_337199dab7.png)

Where each of the a's is one of the elements in the matrix. In software engineering, we would typically encode this information into **an array of arrays**. For example, in Python, it would look something like this:

```python
matrix = [
    [a_1_1, a_1_2, ..., a_1_m], 
    [a_2_1, a_2_2, ..., a_2_m], 
    ..., 
    [a_n_1,a_n_2, ..., a_n_m]
]
```

As defined, matrices could include any type of value under the sun (including mixed types), but for the sake of this article, we will restrict our definition to numeric values. Expanding our focus to include all types would put us squarely in the realm of databases and tabular data, a topic for another day.

**Note:** there is nothing limiting us to a 2d array. **We could expand this to a n-dimensional matrix**. Many matrix libraries also allow us to do this.

## When to Use Matrices in Interviews

As with most data structures, it is unlikely that an interviewer will directly prompt you to use a matrix. With that said it is generally pretty obvious when a matrix should be considered. Oftentimes a problem will be framed on a two-dimensional plane or a grid. You will be asked to extract some information from the grid or to transform the grid in some way.

### Example: Conway's Game of Life

A classic example of this is **Conway's Game of Life**.

![game of life.gif](https://strapi-iio.s3.us-west-2.amazonaws.com/game_of_life_57a715d14e.gif)

You are presented with an n by m grid of 0s and 1s (or a binary matrix). This grid represents the state of the world at a point in time. The 1s are live cells and the 0s represent dead cells. The question is: what will the grid look like at the next timestep? To figure that out we are given the following rules:

- If a cell is dead and…
    - If there are exactly 3 live neighbors (surrounding cells, including corners), the cell becomes alive
    - Otherwise the cell remains dead
- If a cell is alive and…
    - If there are less than 2 or more than 3 neighbors, then the cell dies
    - Otherwise the cell keeps on living.

For more information see:

- Problem [https://leetcode.com/problems/game-of-life/](https://leetcode.com/problems/game-of-life/)
- Interesting Numberphile Video: [https://www.youtube.com/watch?v=R9Plq-D1gEk](https://www.youtube.com/watch?v=R9Plq-D1gEk)

**Note:** Classically Conway's Game of Life is played on an infinite grid.

### Example: Solve a Sudoku

Given a sudoku board (or a matrix partially populated with integers between 1 and 9), use the rules of sudoku to fill in the board.

This problem has a matrix as an underpinning but relies on dynamic programming techniques like recursion and backtracking. Our matrix manipulation and traversal techniques need to be in excellent condition so we can bake them into these more complex algorithms.

For more information see: [https://leetcode.com/problems/valid-sudoku/](https://leetcode.com/problems/valid-sudoku/) [https://leetcode.com/problems/sudoku-solver/](https://leetcode.com/problems/sudoku-solver/) Example: Count the Islands on a Map You are given a grid where each element of the grid is either a 0 (water) or a 1 (land). How many islands are there?

This is a very common type of problem and comes in a number of flavors. At its heart is a graph-inspired search problem. Again, matrix traversal and manipulation are essential to effectively produce a solution.

For more information see: [https://leetcode.com/problems/number-of-islands/](https://leetcode.com/problems/number-of-islands/) [https://leetcode.com/problems/number-of-closed-islands/](https://leetcode.com/problems/number-of-closed-islands/) [https://leetcode.com/problems/island-perimeter/](https://leetcode.com/problems/island-perimeter/)

## Common Mistakes in Interviews Featuring Matrices

### Messy Code

When done carefully, traversing and manipulating **matrices can be a very smooth experience**, but in the turbulent sea of a coding interview, it is easy to get swept into a wave of ugly syntax! Because of this, it is well worth your time to construct helper functions to interact with the matrix directly. Consider methods to help… **Look at all neighboring elements** **Swap rows or columns** **Get all elements of a row or column**

**Creating helper functions like this helps to isolate the sticky bits of your algorithm**. This way if something goes wrong, you don't have to hunt for the broken logic; you will have only one place to look! It's a great practice to go through a matrix-related problem and create some of these helper functions to get a sense of this before the big day.

**Note:** always make sure you are specifying dimensions in the correct order! It is a common practice to need to access an element by specifying the y index and then the x index.

### Altering Values In Place

Many coding questions will want you to alter values in place. Take the example of Conway's Game of Life (detailed above). Finding the state of the board from time step i to i+1 can be done by constructing a new matrix, but this costs additional space. An interviewer could easily ask you to use a single matrix and update values in place. This seems reasonable, right? The problem is each cell needs to look at the surrounding cells to figure out what state it should have. If you are updating the state of surrounding cells you begin losing information! One solution is to use values outside of 0 and 1 to encode additional information. For instance, we could update cells as follows:

- 0 - Was previously 0 and is still 0
- 1 - Was previously 1 and is still 1
- 3 - Was previously 1 and is now 0
- 4 - Was previously 0 and is now 1

Now you might be thinking to yourself, "But we don't want 3s and 4s in our new state!" and you'd be right. We will need to do a second pass on our solution to convert the 3s and 4s into 0s and 1s respectively. Here's an implementation in Python:

```python
from itertools import product

def count_live_neighbors(x: int, y: int, grid: list[list[int]]) -> int:
    """
    Given a position in a grid, count all live neighbors 
    """
    count = 0

    # product allows us to take all combinations of two lists.
    # this allows us to get all combinations of offsets of our element
    for i, j in product([-1,0,1],[-1,0,1]):
        # when i and j are 0 we are looking at element and not a neighbor of the element
        if (i == 0 and j == 0):
            continue

        neighbor_y = y + i
        neighbor_x = x + j

        grid_height = len(grid)-1
        grid_width = len(grid[0])-1

        # don't look past the grid 
        if (neighbor_y < 0 or neighbor_y > grid_height) or (neighbor_x < 0 or neighbor_x > grid_width):
            continue

        # mod by 2 to account for 3s and 4s (updated elements)
        count += grid[neighbor_y][neighbor_x] % 2

    return count

def get_next_state(grid: list[list[int]]) -> None:
    """
    Given a binary grid representing a state in Conway's Game of Life,
    find the state at the next timestamp
    
    Modify the grid in place!
    """
    for y, row in enumerate(grid):
        for x, entry in enumerate(row):
            count = count_live_neighbors(x, y, grid)

            # encode some additional information into our updated grid
            #   1: was a 1 is now a 1
            #   0: was a 0 is now a 0
            #   3: was a 1 is now a 0
            #   4: was a 0 is now a 1
            if entry == 0 and count == 3:
                grid[y][x] = 4
            elif entry == 1 and (count < 2 or count > 3):
                grid[y][x] = 3

    # shift 3s and 4s to their proper value for the new grid state
    for y, row in enumerate(grid):
        for x, entry in enumerate(row): 
            if entry > 1:
                entry -= 3

            grid[y][x] = entry 

    return grid
```

Notice here how the in-place constraint reduced our space complexity but required us to go through our matrix an additional time. While this doesn't increase our big-O time complexity, it does cost real-time. Always keep these tradeoffs in mind!

### Being careless with space

The problems we have talked about up to this point all involved a matrix-like object being manipulated. It isn't hard to imagine a scenario where a matrix is one possible data structure that could be used to solve the problem. Keep in mind that using a matrix can be costly both in terms of time and space! As an example, consider a graph. A typical way to represent a graph is with a Node object which contains pointers to other nodes (this is very similar to how a linked list is constructed). Alternatively, we could represent a graph with an "incidence matrix" where each row/column represents a node in the graph. Connections are represented as a 1 in the matrix (everything else is a 0). A matrix can encode this same information but it is not a very good use of space!

![A Matrix Being Represented as a Graph](https://strapi-iio.s3.us-west-2.amazonaws.com/matrix_graph_4bbba4acb0.png)

Even if a matrix is necessary for your solution keep in mind how costly operations are both in terms of time and space. Adding a single element to a new row or column will cost O(max(n, m)) space. If you need this kind of flexibility a linked structure may be a better tool for the job.

## What to Say in Interviews to Show Mastery Over Matrices

Generally avoiding the pitfalls above will be enough to demonstrate mastery to your interviewer. With that said, learning about the matrix libraries available in your preferred language is important. For example, In Python **Pandas** and **Numpy** are available. Now, it is important to note that while you might be able to implement the same sort of logic from scratch, it will be difficult to squeeze out the same sort of performance that well-established libraries can achieve. These libraries are using low-level tricks to pack values into memory and the CPU cache which can make a big difference to performance! Additionally, many of these libraries can leverage a GPU or TUP to improve performance (see **Tensorflow**). A full explanation of how these low-level languages achieve their performance can be found in the introductory chapter of [Parallel Scientific Computing in C++ and MPI](https://www.amazon.com/Parallel-Scientific-Computing-MPI-Implementation/dp/0521520800).

## Machine Learning and Artificial Intelligence

It is reasonable to say machine learning algorithms would not be where they are today without the help of matrices. Matrices allow calculations rooted in multi-dimensional calculus to be computed quickly. Because of their structure, they fit nicely into memory, and CPUs, GPUs or TPUs can efficiently calculate values rapidly. If you are interested in pursuing a data-focused or machine learning-focused job, diving deeper into this topic will serve you well. Gilbert Strang's treatment of this subject is particularly excellent. An old edition of his book **Introduction to Linear Algebra** or his [MIT open course](https://ocw.mit.edu/courses/18-06-linear-algebra-spring-2010/video_galleries/video-lectures/) ) would be a great place to start.

[[xkcd.com 1838]]