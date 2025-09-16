---
tags:
  - strings
  - datastructure
---
## What are Strings?

![String as an array of characters](https://strapi-iio.s3.us-west-2.amazonaws.com/strings1_f622c456be.png)

Along with arrays, strings are one of the **simplest data structures** out there and are always coming up. Strings can be thought of as a **subset of arrays** because, as simple as they are, strings come with their own set of intricacies ([[Intricacy]]) and challenges. Here are three key properties that we need to remember as we start working with strings.

1. **Under the hood, strings are just an array of characters.** This is important because it affects the time complexities of string methods we might use – keep reading for more details on this!
2. **Like arrays, strings are variable in size.** This one might be obvious given the above point, but it bears repeating. In most languages, arrays are treated as a collection, whereas we think of a string as a single “thing”. However, remember that it’s still **an array of characters in memory**, so the space the string takes up AND it takes a linear amount of time to generate a hash of a string where N is proportional to the length of the string. When discussing time complexities the length of a string plays a factor.
3. **In most languages, strings are [immutable](https://en.wikipedia.org/wiki/Immutable_object#:~:text=In%20object%2Doriented%20and%20functional,modified%20after%20it%20is%20created.).** This is the biggest difference between strings and generic arrays – you can't change them once they are constructed! If you need to update a string you have to rebuild an entirely new string with the update you want. How you avoid this waste of time & space is language dependent. In Java, a StringBuilder is used to hold a stream of characters before converting it to a final immutable string. In Python, it's common to use a list to hold individual characters and then convert it to a string at the very end. Some problems like [Reversing a String](https://leetcode.com/problems/reverse-string/) are commonly solved in [C++](https://interviewing.io/cplusplus-interview-questions), where strings are mutable, but if you are working in a language where strings aren't mutable to follow the spirit of this question it requires you to "fake" string mutability by first converting your string to a list then pretending your language can mutate strings directly.

## Common Mistakes in Interviews Featuring Strings

### Viewing String Problems As "Easy"

Strings, despite being one of the first data structures introduced to programmers, shouldn't be underestimated as "easy" in interview scenarios due to their versatility. Unlike data structures like trees or graphs that have specific algorithms like DFS/BFS or backtracking respectively, strings can incorporate a range of technical topics frequently asked in interviews. **Strings are a linear data structure**, and because of that **all common algorithms related to linear data structures could potentially be involved in a string question**. This means techniques like [two pointers](https://interviewing.io/two-pointers-interview-questions), [sliding windows](https://interviewing.io/sliding-window-interview-questions), [recursion](https://interviewing.io/recursion-interview-questions), backtracking, and [dynamic programming](https://interviewing.io/dynamic-programming-interview-questions) (to name just a few) **can be used in a string question**. Therefore, avoiding string practice due to perceived ease could lead to challenges in handling complex string problems in interviews.

### Messing Up String Conversions

One of the more annoying things we can have to do, which nevertheless comes up fairly often, is various forms of string math. This includes **converting characters to their index in the alphabet** and **converting characters to their numeric value**. General familiarity with how to do these things in your interviewing language is critical. It's obscure enough to not remember on the spot, but simple enough that it looks bad if you don't know how to do it.

### Making Assumptions About String Contents

It's easy to think of strings as just letters in the alphabet, but this will lead to one of the most common interview errors with string questions – making an incorrect assumption about the string contents. Useful clarifying questions to ask whenever strings are involved in a problem can be questions like.

- Are we **guaranteed that there will just be alphabetical characters**? **Alphanumeric**?
- Do we need to worry about **punctuation**?
- Do I need to handle **special characters/symbols**?
- Can the string ever be **empty** or **null**?
- Is the string **always lower/uppercase**? Can we receive a **mixed case string**?
- Do we need to worry about the **string encoding** at all? **UTF-8**, **ASCII**, etc?
- Does the **string fit into memory**?

Here's a good example of a string question where [all of these questions matter](https://leetcode.com/problems/ransom-note/) in achieving the correct output to pass all tests. Don't make assumptions about what is in the string, **asking these types of questions helps demonstrate your seniority** and **familiarity with common gotchas**.

### Hidden Complexity

One danger you should be aware of is how languages will abstract away the heavy lifting when it comes to strings. This can make us wrongly assume that "simple" operations are cheap. For example, we can very easily get a substring of a string in **Python** using the Python slicing syntax: s[1:5]. Writing it this way we may assume that this is a constant-time operation. However, **in most cases, operations like this are still going to copy the substring (remember strings are immutable), meaning that it is going to take us linear time**.

One great feature of **Java is the StringBuilder class**. This class provides a performant way to modify and append onto a string by using an array as the underlying data structure. StringBuilder also **provides a nice toString() method that we can use to recover a string**.

**C uses an array as the underlying data structure which prevents the language from masking additional complexity**. With that said, we have to be **careful when allocating an array in C**. The size of the array is static which **means all of the memory needs to be allocated up front**!

|**String Operation**|**Description**|**Time**|**Space**|
|---|---|---|---|
|Length|Returns the number of characters in the string.|`O(1)`|`O(1)`|
|Index Access|Accesses a character at a specific position in the string.|`O(1)`|`O(1)`|
|Concatenation (`+`)|Combines two strings into one.|`O(n)`|`O(n)`|
|Traversal (e.g. `for` loop)|Goes through each character in the string one by one.|`O(n)`|`O(1)`|
|Naive Search (e.g.  <br>`contains`, `index of`)|Searches for a specific character or substring in the string.|`O(n*m)`|`O(1)`|
|Substring|Creates a new string that is a subset of the original string.|`O(m)`|`O(m)`|

- `n` represents the length of the string
- `m` represents the length of the substring

This above table is a generalized view of string operations, but it's worth mentioning that the details will differ depending on your particular language. For example, in some Java versions, the substring operation was `O(1)` in space complexity as it shared the same character array with the original string, but this has been changed in more recent versions to avoid memory leaks, leading to `O(s)` space complexity, with `m` as the length of the substring.

## Advanced String Topics

### The Multiple Pointers Technique

Same as with arrays, it is common to use multiple pointers to traverse a string. This allows us to accomplish various interesting tasks with substrings and comparing characters. Here are some problems to consider:

- [Reverse words in a string](https://interviewing.io/questions/reverse-words-in-a-string)
- [String compression](https://leetcode.com/problems/string-compression/)

### The Sliding Window Technique

[**Sliding windows**](https://interviewing.io/sliding-window-interview-questions) are common with any linear data structure. That includes things like arrays, linked lists, and, of course, strings. They are a great tool for finding the longest substring matching an arbitrary property. For practice take a look at the following.

- [Longest substring without repeating characters](https://interviewing.io/questions/longest-substring-without-repeating-characters)
- [Longest substring with at least k repeating characters](https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/)
- [Find all anagrams in a string](https://leetcode.com/problems/find-all-anagrams-in-a-string/)

### Advanced String Algorithms

These advanced algorithms are fairly niche and only likely to be asked at FAANG companies, and even then these algorithms show up a small fraction of the time. If you want to go deep on strings, there are three advanced algorithms worth having on hand. All of these algorithms are used for searching for a substring within a string and variations of them exist in a handful of problems online. The core algorithms to learn are:

- [KMP](https://en.wikipedia.org/wiki/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm)
- [Boyer Moore](https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_string-search_algorithm)
- [Rabin-Karp](https://en.wikipedia.org/wiki/Rabin%E2%80%93Karp_algorithm)

### Regular Expressions

While it is unlikely that you will get a problem which can be solved directly with regular expressions, you should have a good idea of how regular expressions work. Leetcode questions with regular expression answers [do exist](https://leetcode.com/problems/solve-the-equation/description/), but are uncommon. If you're thinking of using regular expressions in your solution, you're probably over-complicating it. With that stated, it is still important to have familiarity with them. Consider playing with a site like [regex101.com](http://regex101.com/) to develop a better sense of regular expressions. Additionally, spend some time thinking through how to document a regular expression. **Demonstrating not just an understanding of regular expressions** but **how to make them maintainable shows a certain coding maturity**.

## Language-Specific Advice

Up to this point, all the advice we have given has been language agnostic but various languages handle strings very differently. In this section, we will cover features of four popular language choices: Java, C++, Python & JavaScript.

### Java Strings

**Fast Facts:**

- Mutable? No
- Primitive? No
- Comparison: `s1.equals(s2)`
- Access the ith character: `s1.charAt(i)`

**Useful Java String Methods:**

|**Method**|**Description**|**Time**|**Space**|
|---|---|---|---|
|`[s.length()](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/lang/String.html#length\(\))`|Returns the length of the string|`O(1)`|`O(1)`|
|`[s.charAt(int i)](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/lang/String.html#indexOf\(java.lang.String\))`|Returns the character at index `i`|`O(1)`|`O(1)`|
|`[s.substring(int i, int j)](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/lang/String.html#contains\(java.lang.CharSequence\))`|Returns substring from `i` to `j` (inclusive of `i`, exclusive of `j`)|`O(j-i)`|`O(j-i)`|
|`[s.contains(String s)](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/lang/String.html#substring\(int,int\))`|Returns `True` if `s` is contained in the string|`O(1)`|`O(1)`|
|`[s.indexOf(String s)](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/lang/String.html#charAt\(int\))`|Returns the starting index of the first occurrence of `s`|`O(n)`|`O(1)`|

In Java, there are some common points to be aware of…

```java
/* Strings are OBJECTS */
// Primitives in Java are lowercase and include data types like:
double foo = 76.762121;
char bar = 'i';
boolean baz = true;

// Strings are *Objects*
String s = "Interviewing.io";


/* String comparison doesn't use the == operator */
String a = "Interview";
String b = "Interview";

// This outputs false because == compares the Object pointers not values
System.out.println(a == b); 
// This outputs true because equals() compares the values of the strings
System.out.println(a.equals(b));


/* Comparing Object pointers uses the == operator */
String c = a;
// This outputs true since a and b point to the same object in memory
System.out.println(a == c);
```

### C++ Strings

**Fast Facts:**

- Mutable? No
- Primitive? No
- Comparison: `s1.compare(s2)`
- Access the ith character: `s1[i]`

**Useful C++ String Methods:**

|**Method**|**Description**|**Time**|**Space**|
|---|---|---|---|
|`[s.length()](https://cplusplus.com/reference/string/string/length/)`|Returns the length of the string `s` (from string::length)|`O(1)`|`O(1)`|
|`[s1.find(s2)](https://en.cppreference.com/w/cpp/string/basic_string/find)`|Returns the index of `s1` in the string `s2` (from string::find)|`O(s1 * s2)`|`O(1)`|
|`[strcpy(chars, s.c_str())](https://en.cppreference.com/w/cpp/string/byte/strcpy)`|Converts `s1` into a character array|`O(n)`|`O(n)`|
|`[s.substr(i, j)](https://en.cppreference.com/w/cpp/string/basic_string/substr)`|Get the substring of `s` from `i` with length `j`|`O(j)`|`O(j)`|

The largest difference between strings in Java and C++ is that strings are mutable in C++. See below for details!

```c++
#include <iostream>
#include <string>

int main() {
    // Primitive types
    double foo = 76.762121;
    char bar = 'i';
    bool baz = true;

    // Strings are not a primitive in C++. They are an object of std::string class
    std::string a = "Interviews";
    std::string b = "Interviews";

    // Comparing strings using compare()
    // Returns 0 since strings are equal
    if(a.compare(b) == 0){
      std::cout << "You will see this because both strings are identical";
    }

    // Comparing strings using == operator
    if(a == b){
      std::cout << "You will see this because both strings are identical";
    }

    // Strings are mutable in C++
    std::string c = str1;

    c[9] = 'z'; // attempt to modify the last letter of string works!
    std::cout << c; // will print "Interviewz"
    
    return 0;
}
```

### Python Strings

**Fast Facts:**

- Mutable? No
- Primitive? Yes and no, but mostly no. "Primitive" isn't a word in Python, all types are objects!
- Comparison: `s1 == s2`
- Access the ith character: `s1[i]`

**Useful Python String Methods:**

|**Method**|**Description**|**Time**|**Space**|
|---|---|---|---|
|`[len()](https://docs.python.org/3/library/functions.html#len)`|Returns the length of the string|`O(1)`|`O(1)`|
|`[s1 in s2](https://docs.python.org/3/reference/expressions.html#membership-test-operations)`|Is `s1` a substring of `s2`|`O(s1 * s2)`|`O(1)`|
|`[s1.index(s2)](https://docs.python.org/3/library/stdtypes.html#str.index)`|Returns the index of the first occurrence of `s2` in the string, ValueError if not found|`O(s1)`|`O(1)`|
|`[list(s)](https://docs.python.org/3/library/stdtypes.html#str.__iter__)`|Converts `s1` into a list of characters|`O(n)`|`O(n)`|
|`[s[i:j]](https://docs.python.org/3/reference/datamodel.html#slicings)`|Get the substring of `s` from `i` (inclusive) to `j` (exclusive)|`O(j-i)`|`O(j-i)`|

In typical Python fashion, this is probably the easiest of these four languages to handle strings. Rather than having to use a lot of function calls, much of what we might want to do is built into the language, such as getting substrings of a string. However, you should use caution when using Python, the simplicity of the language often masks underlying complexity.

```python
# All types in Python are objects
foo = 76.762121
bar = 'i'
baz = True
a = "Interviews"
b = "Interviews"
print(type(foo)) # <class 'float'>
print(type(bar)) # <class 'str'>
print(type(baz)) # <class 'bool>
print(type(a))   # <class 'str>

# Comparing strings in Python
print(a == b) # True

# Strings are immutable in Python
a[9] = 'z' # TypeError: 'str' object does not support item assignment
```

### JavaScript Strings

**Fast Facts:**

- Mutable? No
- Primitive? Yes
- Comparison: `s1 == s2` and sometimes `s1 === s2` (see below for details)
- Access the ith character: `s1[i]`

**Useful JavaScript String Methods:**

|**Method**|**Description**|**Time**|**Space**|
|---|---|---|---|
|`[s.length()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/length)`|Returns the length of the string|`O(1)`|`O(1)`|
|`[s2.includes(s1)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/includes)`|Is `s1` a substring of `s2`|`O(s2)`|`O(1)`|
|`[s.indexOf(searchValue)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/indexOf)`|Returns the index of the first occurrence of `searchValue`|`O(1)`|`O(1)`|
|`[s.split(separator)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split)`|Splits the string into an array of substrings based on the separator|`O(1)`|`O(1)`|
|`[s.join(separator)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join)`|Joins the elements of an array into a string using the separator|`O(1)`|`O(1)`|
|`[s.substring(i, j)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substring)`|Get the substring of `s` from `i` (inclusive) to `j` (exclusive)|`O(1)`|`O(1)`|

JavaScript strings share some similarities with other languages but also have their unique characteristics. In JavaScript, strings are primitive values but have access to several built-in methods that allow manipulation and retrieval of string data. It's important to note that JavaScript strings are immutable, meaning that once a string is created, it cannot be changed. Instead, operations on strings return new strings.

When comparing strings in JavaScript, the strict equality operator `(===)` is used to compare both the value and the type of the string. This ensures an accurate comparison of two strings. To access individual characters within a string, the `charAt()` method is used.

JavaScript provides various useful methods for working with strings, such as `length` to retrieve the length of a string, `substring` to extract a portion of a string, `includes` to check if a substring is present, `indexOf` to find the index of a substring, `split` to split a string into an array based on a separator, and `join` to concatenate array elements into a single string using a separator.

Be sure to be particularly mindful of string immutability in JavaScript, since string update operations will compile successfully and fail silently like the below example illustrates:

Javascript

```javascript
let str = "ab";

// attempting to swap 'a' and 'b'
let temp = str[0]
str[0] = str[1]; // operation does nothing and fails silently!
str[1] = temp; // operation does nothing and fails silently!
console.log(str); // still "ab"!!!
```

Overall, JavaScript offers a range of methods and functionalities for handling strings, making it a versatile language for string manipulation tasks.