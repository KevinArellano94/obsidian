---
tags:
  - parsing
  - datastructure
---
## What is Parsing?

Parsing problems are a very special subset of string problems. Here we are reading a file or a file-like object and using syntax rules to convert the file into a data structure. This process is commonly used by compilers and interpreters, but it can also be used for other things, such as natural language processing.

The process of parsing is typically broken up into two separate processes: **tokenization** and **parsing**. Notice that parsing both **refers to the whole process** and **one of the steps**.

**Tokenization** is when the **file is processed and consecutive characters are grouped together to form tokens**. A **token** can be thought of as **a word**. These can be a **single character** or a **group of characters** and will later, in the parsing process, have meaning inside of the context of the file's syntax. For instance the code `for i in range(1, 100)` could be broken up into the following tokens: `for`, `i`, `in`, `range`, `(`, `1`, `,` , `100`, `)`. The **tokenizer strips out the white spaces** and **determines which characters should be clumped together**.

Once the tokens have been processed, the parser will build out a hierarchy tree of expressions. At each level of the hierarchy, we have an expression containing a bunch of tokens. We will **continue breaking expressions down until we cannot divide them anymore**. When we cannot divide an expression further it is known as a **terminal expression**. Take this example from Wikipedia ([https://upload.wikimedia.org/wikipedia/commons/a/ac/Python_add5_parse.png](https://upload.wikimedia.org/wikipedia/commons/a/ac/Python_add5_parse.png)). Here the following Python function is displayed as a syntax tree:

```python
def add5(x):
	return x + 5
```

![[Pasted image 20250913230140.png]]

As we will see in the next section, having a comprehensive knowledge of parsing is not necessary to pass a coding interview. With that said, this knowledge will help you to frame the problem and make the mountain feel much more climbable.

## When to Use Parsing in Interviews

There are a couple of places where you might need to use parsing in a coding interview. In the first case, you are **presented with a file that needs to be parsed** and **you must write the parsing engine from the ground up**. For a problem like this, it is likely that the grammar rules will be very simple since more complex examples will require time you don't have.

You might also need to **parse a file when you’re ingesting** a file, as part of a larger process. In cases where the parser isn't the star of the show, **it is unlikely that the interviewer will want you to spend time standing something up**, rather you will be **expected to recommend a library**, e.g., using Python’s built-in json module when parsing a JSON file.

In the context of a systems design interview, it is unlikely that you will need parsing and you will certainly not need the details of the algorithm. If anything it will be a footnote of your design, something like "this node will handle the parsing of incoming files.”

### Example (Mini Parser)

**Link:** [https://leetcode.com/problems/mini-parser/](https://leetcode.com/problems/mini-parser/)

In this problem, you are given a serialized string s containing nested lists of integers (for example: `"[1,[1,2,[5,6]],[3,4]]"`). You need to turn this into the corresponding data structure. **The most challenging part of this problem is tracking scope as you process the string**. To do this, **consider using an int to track scope depth**. Every time you encounter a `"["`, **add 1 to the depth**, and every time you encounter a `"]"`, **subtract 1**. This also **gives you an excellent way of looking for malformed strings**.

## Common Mistakes in Interviews Featuring Parsing

### Reinventing the Wheel

If you are given the problem of parsing an arbitrary file, you will likely need to build a parser from the ground up. However, if you need to parse a config file specifically and getting what you need out of that file is just part of a bigger problem, **always check if you can use existing machinery**. **Leveraging existing libraries** shows that y**ou are thinking of the most efficient solution**.

### Defining Scope

Parsing a file can be a very involved task. Depending on the grammar that you are creating a parser for, your job may take weeks or even months. With this in mind, **it is important to establish exactly what your interviewer is looking for** and to **call out expected limitations**.

### Handling Edge Cases/Errors

When processing input that can take so many forms, it is easy for edge cases to sneak in. Make sure to **spend some time quizzing your interviewer about what the input could look like**. Establishing this upfront will **ensure your solution is flexible enough**. Some examples of edge cases include:

- **Whitespace** - Most of the time we want to ignore whitespaces but languages like Python also use whitespace to define scope. Quoted Text - In many files, **you will want to treat anything inside quotes like a single token**.
- **Comments** - Many languages allow comments to be added to the code. Depending on the needs of your parser this may be ignored, or you may have rules for how to handle it. For instance, if your parser is responsible for generating documentation, comments could be very important.

Additionally, spend some time discussing **how errors should be handled**. Do you want the pro**gram to halt** or, like HTML, do you want your program to **pretend like everything is fine** and **proceed as best you can**?

## What to Say in Interviews to Show Mastery Over Parsing

![[Pasted image 20250914012232.png]]

Credit: https://xkcd.com/1090/

**Showing expertise in the domain** of parsing means **going beyond handling the simple examples you are most likely to see**. While you will not be expected to come up with a robust solution on the spot, **understanding parsing at a deeper level** will aid you greatly when **talking through your solution**. You will be able to **pull concepts that communicate** to the interviewer your expertise in this area. With that in mind, it would be worth diving deeper. Here are some resources to get you started:

- [Abstract Syntax Trees](https://en.wikipedia.org/wiki/Abstract_syntax_tree)
- [Parse Trees](https://en.wikipedia.org/wiki/Parse_tree)
- [Context-Free Grammar](https://en.wikipedia.org/wiki/Context-free_grammar)
- [Lexical Analysis (or Tokenization)](https://en.wikipedia.org/wiki/Lexical_analysis)
- Writing a Parser
    - [Part 1](https://supunsetunga.medium.com/writing-a-parser-getting-started-44ba70bb6cc9)
    - [Part 2](https://supunsetunga.medium.com/writing-a-parser-algorithms-and-implementation-a7c40f46493d)
    - [Part 3](https://supunsetunga.medium.com/writing-a-parser-syntax-error-handling-b71b67a8ac66)