## Chapter 1

Which algorithm is best for a given application depends on - among other factors - the number of items to be sorted, the extent to which the items are already somewhat sorted, possible restrictions on the item values, the architecture of the computer, and the kind of storage devices to be used: main memory, disks, or even - archaically - tapes.

Examples of problems that make essential use of algorithms include finding good routes on which the data travels (techniques for solving such problems appear in Chapter 22), and using a search engine to quickly find pages on which particular information resides (related techniques are in Chapters 11 and 32).

Public-key cryptography and digital signatures **numerical algorithms** and **number theory** (Chapter 31).

Allocate scarce resources, maximize expected profit, maximize chance of winning election, assign crews to flights in the least expensive way, etc... can be solved modeling them as **linear program** (Chapter 29).

Graphs (Chapter 22).

Mechanical design for library of parts using **topological sorting** (Chapter 20).

Image processing to detect cancerous/benign tumors with **clustering algorithm** (Chapter 33).

Large file compression using "**Huffman coding**" (Chapter 15).

**Fourier transformation (FFT) algorithm** (Chapter 30).

A **data structure** is a way to store and organize data in order to facilitate access and modifications. Using the appropriate data structure or structures is an important part of algorithm design.

Measure of efficiency: speed. How long does an algorithm take to produce it's results? **NP-complete** (Chapter 34).

**Approximation algorithms** (Chapter 35).

In order to elicit the best performance from multicore computers, we need to design algorithms with parallelism in mind, "**Task-parallel**" (Chapter 26).

Scheduling algorithms, example, future vehicle and online traffic routing, hospital triaging decisions, airports require not relying on future input to do their jobs, **online algorithms** (Chapter 27).

### Exercises
#### 1.1-1
Describe your own real-world example that requires sorting. Describe one that requires finding the shortest distance between two points.
- Data stored in databases for fast lookup to utilize binary search tree.
- Navigation
#### 1.1-2
Other than speed, what other measures of efficiency might you need to consider in a real-world setting?
- space complexity (memory is finite)
- processing power (only so many processing cores)
- cost
#### 1.1-3
Select a data structure that you have seen, and discuss its strengths and limitations.
- sorting algorithm, great at lookup/insertion, but depends on data structure and data being sorted
- weighted graphs, great at finding shortest path, requires traversing all of the points if not done correctly
#### 1.1-4
How are the shortest-path and traveling-salesperson problems given above similar? How are they different?
- Requires graphs and vertices.
- Also requires to visit all points at least once (Hamiltonian cycle).
#### 1.1-5
Suggest a real-world problem in which only the best solution will do. Then come up with one in which "approximately" the best solution is good enough.
- Space missions.
- Route planning for delivery.
#### 1.1-6
Describe a real-world problem in which sometimes the entire input is available before you need to solve the problem, but other times the input is not entirely available in advance and arrives over time.
- Future vehicle and online traffic routing.
- Hospital triaging decisions.
- Airports.

Good software engineering practice:
- well designed
- documented

Computing time is bounded resource, making it precious.
"Time is money" - you can get back money after you spend it, but once time is spent, you can never get it back.

Algorithms, juts like computer hardware, is technology.

For a concrete example, let us pit a faster computer (computer A) running insertion sort against a slower computer (computer B) running merge sort. They each must sort an array of 10 million numbers. (Although 10 million numbers might seem like a lot, if the numbers are eight-byte integers, then the input occupies about 80 megabytes, which fits in the memory of even an inexpensive laptop computer many times over.) Suppose that computer A executes 10 billion instructions per second (faster than any single sequential computer at the time of this writing) and computer B executes only 10 million instructions per second (much slower than most contemporary computers), so that computer A is 1000 times faster than computer B in raw computing power. To make the difference even more dramatic, suppose that the world’s craftiest programmer codes insertion sort in machine language for computer A, and the resulting code requires 2n2 instructions to sort n numbers. Suppose further that just an average programmer implements merge sort, using a high-level language with an ineffecient compiler, with the resulting code taking 50 n lg n instructions. To sort 10 million numbers, computer A takes

$$
\frac{2 \cdot (10^7)^2}{10^{10} \text{ instructions/second}} = 20,000 \text{ seconds (more than 5.5 hours)},
$$

while computer B takes

$$
\frac{50 \cdot 10^7 \lg 10^7}{10^7 \text{ instructions/second}} \approx 1163 \text{ seconds (under 20 minutes)}.
$$

### Exercises
#### 1.2-1
Give an example of an application that requires algorithmic content at the application level, and discuss the function of the algorithms involved.
- Machine learning, since all it is are collection of algorithms.
#### 1.2-2
Suppose that for inputs of size n on a particular computer, insertion sort runs in 8n2 steps and merge sort runs in 64 n lg n steps. For which values of n does insertion sort beat merge sort?

$$
\frac{2 \cdot (8^7)^2}{10^{10} \text{ instructions/second}} = 20,000 \text{ seconds (more than 5.5 hours)},
$$
$$
\frac{64 \cdot 8^7 \lg 8^7}{10^7 \text{ instructions/second}} \approx 1163 \text{ seconds (under 20 minutes)}.
$$
#### 1.2-3
What is the smallest value of n such that an algorithm whose running time is 100n2 runs faster than an algorithm whose running time is 2n on the same machine?
- n = 15
#### 1-1 Comparison of running times
For each function `f(n)` and time t in the following table, determine the largest size n of a problem that can be solved in time t , assuming that the algorithm to solve the problem takes `f(n)` microseconds.

1000000 microseconds in a second


|            |               1 second |                  1 minute |                       1 hour |                        1 day |                       1 month |                         1 year |                         1 century |
| ---------: | ---------------------: | ------------------------: | ---------------------------: | ---------------------------: | ----------------------------: | -----------------------------: | --------------------------------: |
|    $\lg n$ | $\approx 10^{301,030}$ | $\approx 10^{18,061,800}$ | $\approx 10^{1,083,708,000}$ | $\approx 10^{2,600,899,200}$ | $\approx 10^{78,026,976,000}$ | $\approx 10^{949,423,872,000}$ | $\approx 10^{94,942,387,200,000}$ |
| $\sqrt{n}$ |              $10^{12}$ |       $3.6 \cdot 10^{15}$ |        $1.296 \cdot 10^{19}$ |       $7.4656 \cdot 10^{21}$ |      $6.718464 \cdot 10^{24}$ |     $9.94599296 \cdot 10^{27}$ |        $9.94599296 \cdot 10^{31}$ |
|        $n$ |                 $10^6$ |            $6 \cdot 10^7$ |             $3.6 \cdot 10^9$ |         $8.64 \cdot 10^{10}$ |         $2.592 \cdot 10^{12}$ |         $3.1536 \cdot 10^{13}$ |            $3.1536 \cdot 10^{15}$ |
|  $n \lg n$ |       $\approx 62,708$ | $\approx 3.35 \cdot 10^6$ |    $\approx 1.33 \cdot 10^8$ |    $\approx 2.87 \cdot 10^9$ |  $\approx 7.02 \cdot 10^{10}$ |   $\approx 7.54 \cdot 10^{11}$ |      $\approx 6.34 \cdot 10^{13}$ |
|      $n^2$ |                $1,000$ |           $\approx 7,746$ |             $\approx 60,000$ |            $\approx 294,000$ |           $\approx 1,610,000$ |            $\approx 5,620,000$ |              $\approx 56,200,000$ |
|      $n^3$ |          $\approx 100$ |             $\approx 391$ |              $\approx 1,533$ |              $\approx 4,420$ |              $\approx 13,740$ |               $\approx 31,600$ |                 $\approx 146,600$ |
|      $2^n$ |                   $19$ |                      $25$ |                         $31$ |                         $36$ |                          $41$ |                           $44$ |                              $50$ |
|       $n!$ |                    $9$ |                      $12$ |                         $15$ |                         $17$ |                          $17$ |                           $22$ |                              $25$ |
