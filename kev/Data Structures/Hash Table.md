---
tags:
  - hashtable
  - datastructure
  - keyvalue
---
## What is a Hash Table?

A hash table is a **key-value data structure**. Keys are typically able to be accessed in **amortized constant time** and values can be **single items** or more commonly a **list of items**.

### Hashtables, Hashmaps, and Dictionaries. Oh My!

Most languages have built-in key-value pair data structures, but each language will have different names, terminology, and even different implementations associated with them. All languages provide efficient ways to store, retrieve, and manipulate data because they allow for near-instant access to the data associated with a specific key. While there is little consistency for what a key-value data structure is called between languages, for the sake of this article we will use the term "hash table" to encompass the following:

- Hash Table (sometimes a single word: "Hashtable")
- Hash Map (sometimes a single word: "Hashmap")
- Map
- Dictionary

In [Python](https://interviewing.io/python-interview-questions), these structures are referred to as dictionaries (or "dicts"). In [JavaScript](https://interviewing.io/javascript-interview-questions), before ES6 these were represented as a general Object but after ES6 we now have a dedicated Map object. [C++](https://interviewing.io/cplusplus-interview-questions), on the other hand, includes both map and unordered_map in its Standard Template Library (STL), the latter being equivalent to a hash table. In Java, they are usually called Maps, represented by the Map interface which has several implementations including HashMap and TreeMap (but many more exist). Confusingly, Java has both a Hashtable and a HashMap. The main differences between them are that **HashMap is multi-threaded and therefore not thread-safe** and also **allows for a null key** & **null values**. The **Hashtable implementation is thread safe** and **doesn't allow null keys or values**.

### Comparing Hash Tables, Arrays, and Sets

It's not uncommon for candidates to understand the differences between these three data structures yet fail to select the correct data structure in an interview context. Here is a brief comparison of these data structures and how they relate to one another. In general we should…

- Use **Arrays** when we need to **store elements of the same type**, in a **particular order**, or we need to **frequently access** them **by their index**.
- Use **Hash tables** when we need to **store key-value pairs** and **perform frequent lookup**, **insert**, or **delete** operations.
- Use **Sets** when we need to **store unique elements**, **don't care about duplicates**, and just need to perform operations like **checking if an element is in the set or not**.

|                         | **Arrays** | **Hash Tables**           | **Sets**                  |
| ----------------------- | ---------- | ------------------------- | ------------------------- |
| **Access**              | O(1)       | O(1) avg, O(n) worst-case | O(1) avg, O(n) worst-case |
| **Search**              | O(1)       | O(1) avg, O(n) worst-case | O(1) avg, O(n) worst-case |
| **Insertion**           | O(1)       | O(1) avg, O(n) worst-case | O(1) avg, O(n) worst-case |
| **Deletion**            | O(1)       | O(1) avg, O(n) worst-case | O(1) avg, O(n) worst-case |
| **Key-Value Pairs**     | No         | Yes                       | No                        |
| **Unique Elements**     | No         | Keys are unique           | Yes                       |
| **Additional Metadata** | No         | Yes                       | Yes                       |
| **Memory Usage**        | Low        | High                      | High                      |

- `n` represents the size of the data structure

## How Does a Hash Table Work?

Did you know that a hash table is actually **just an array under the hood with some helper methods**? It's true! Picture a **super-organized parking lot (our array)** and a **hard-working valet (our hash function)**. You **hand the valet your car keys**, and **he decides where to park your car**. The valet has a unique system where he uses the key to choose a parking spot. That's exactly what a hash table does!

A good hashing function can make a big difference in how efficiently we can look up data. For example, what if two cars (keys) are assigned the same spot? That's a collision! In the programming world, we have some neat strategies to handle those.

With "**separate chaining**", the parking spot just grows a little garage (a linked list) and parks the cars (hash table "keys") one behind the other.

"**Open addressing**", on the other hand, is like the valet looking for the next available spot. If we are parking the cars **right next to one another then that's "linear probing"**. If the valet starts hopping around in a specific pattern then it is **quadratic probing** or **double hashing** in the CS world.

Imagine our valet is having a bad day and just trying to park all the cars as close together in the same spot as possible, causing a traffic jam, or putting all the cars so far away it takes forever to get to them. This will result in a lot of collisions and will make a mess! That's like a poor hash function in coding. A good hash function, like a top-notch valet, parks the cars in a way that they're spread out evenly (avoiding traffic jams or "collisions") and are easy to retrieve when needed.

Now imagine that our parking lot is getting filled up. This is when "**rehashing**" comes in. It's like the valet suddenly puts in an order for a bigger parking lot, moves all the cars around to space them out more, reducing the chances of assigning two cars to the same spot.

Even though finding a parking spot (or an array index!) might sometimes take longer than expected, over many trips to the lot (or "amortized over time"), our valet (hash function) usually gets us there pretty quickly, averaging out to constant time. Here's a little python code as an example. The code supports a fixed size table of 10 elements and does not rehash when the table gets full and just continues to use separate chaining to avoid collisions (eventually degrading performance).

```typescript
export class HashTable {
    size: number;
    table: [][];
    constructor() {
        this.size = 10;
        this.table = new Array(this.size).fill(null).map(() => []);
    }

    hashFunction(key: number) {
        return key % this.size;
    }
  
    insert(key: number, value: any) {
        const hashIndex = this.hashFunction(key);
        let keyExists: boolean = false;
        let bucket: any[] = this.table[hashIndex];
  
        for (let i = 0; i < bucket.length; i++) {
            if (bucket[i][0] === key) {
                keyExists = true;
                bucket[i] = [key, value];
                break;
            }
        }
  
        if (!keyExists) bucket.push([key, value]);
    }
}
  
if (import.meta.main) {
    const hashtable = new HashTable();
    hashtable.insert(0, `test-value`);
}
```

## When to Use a Hash Table in an Interview?

When it comes to technical interviews, problems often revolve around **manipulating** and **processing data**. One of the **most common ways to speed up an algorithm is to trade time for space**. Phrased differently, we can **increase the speed of many algorithms** if we are **willing to store some extra data in memory** to **avoid an expensive lookup operation later**. This is the primary use for hash tables.

Hash tables tend to be used in conjunction with other techniques to solve a problem, rather than being a solution in themselves. Figuring out what to save as the key and value and then how to use that information once saved is more difficult than understanding the concept itself. Here are some well-known scenarios where these structures tend to be most useful:

### Frequency Counts

It's a fairly common requirement in interview problems to **count the frequency of something**. We use the key to hold the unique element we are tracking (whether it is a letter, string, or even an entire object) and the value is used to hold the number of times we've seen it. This usually allows us to eliminate the need for a nested loop, thereby saving us time. Here are a few example problems showcasing this.

- [Top K Frequent Elements](https://interviewing.io/questions/top-k-frequent-elements): A hash table can be used to count the **frequency of each element**, then a **heap** or another **sorting algorithm can be used to select the top k**.
- [Ransom Note](https://leetcode.com/problems/ransom-note/): A hash table can be used to count the **frequency of each character in the magazine**.
- [Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/): A hash table can be used to **count the frequency of each character in p**, and then a **sliding window can be used to track the frequency of characters in s**.
- [First Unique Character In a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/): A hash map can be used to count the **frequency of each character**, though a **set may be a slightly better data structure** here to save a small amount of space.

Pro Tip: In Python, there are two common tools you can utilize in `collections` to save yourself time in an interview.

A `Counter` can count the frequency of elements occurring in a list (note the capitalization!)

```typescript
/*
There is no direct equivalent for the python Counter in JavaScript.
The closest approximation is to use JavaScript's array methods or
objects to count occurrences of words. See below for an example of that.
*/
if (import.meta.main) {
    const words: string = "i love love love interviewing.io";
    const wordsArray = words.split(" ");
  
    const counter = wordsArray.reduce((acc: any, word: any) => {
        acc[word] = (acc[word] || 0) + 1;
        return acc;
    }, {});
  
    console.log(counter); // { i: 1, love: 3, 'interviewing.io': 1 }
}
```

More generally, a `defaultdict` can initialize default values for you when adding a new key to your hash table (aka dictionary).

```typescript
/*
There is no direct equivalent to Python's collections.defaultdict.
However, we can achieve similar functionality by using the logical
OR (||) operator to provide a default value when a key doesn't exist
in the dictionary.
*/
const words: string = "i love love love interviewing.io";
const dictionary = {};
for (const word of words.split(" ")) {
    dictionary[word]: any = (dictionary[word] || 0) + 1;
}

console.log(dictionary); // { i: 1, love: 3, 'interviewing.io': 1 }
```

### Data Tracking and Organization

Sometimes it's easier to track data when it is logically grouped together. This tends to also increase the efficiency of your lookups of the data but is useful on its own even if you don't need that efficiency. This may be the most common way to use hash tables – in problems where we need to track the location of something like a character, index, or node.

- Classic examples would be problems like [Two Sum](https://interviewing.io/questions/two-sum) and [Three Sum](https://interviewing.io/questions/three-sum) where we track the number with the key and track where the number occurred in the array with the value.
- This common pattern can also apply to index ranges where you keep track of something between a particular start and end index. This is the basic idea behind a more advanced strategy known as prefix & suffix array tracking.
- A final index location problem example is the popular [Least Recently Used (LRU) Cache](https://interviewing.io/mocks/microsoft-python-lru-cache) problem. This is the most popular question on LeetCode and well worth your time to look at if you aren't familiar with it. The clever optimal solution involves a doubly-linked list and a hash table to track the locations of the elements in the linked list.

### Graph Representations

Similar to the above, but worth calling out on its own, **hash tables can efficiently represent a graph by storing vertices as keys and their adjacency list as values**. This allows **quick access to each vertex's adjacent vertices**, **facilitating traversal** and **other operations**. Additionally, extra information such as **vertex weight can be stored in the value**, enabling a **wide range** of **graph algorithms**.

Using a hash table for this purpose offers several benefits. The primary **advantage is the `O(1)` average time complexity** for **lookups**, **insertions**, and **deletions** that hash tables offer. This means that **accessing a vertex's adjacency list**, **adding a new vertex**, or **deleting a vertex can be done very quickly**, **regardless of the size** of the graph.

For instance, if you want to find all the vertices adjacent to a specific vertex, you can access the adjacency list directly using the hash table. Similarly, if an edge is added or removed, updating the adjacency list is quick. Here's an example hash table in Python representing a simple undirected graph in the form of an adjacency list. The graph has four vertices (A, B, C, and D) and 5 edges ((A-B), (B-C), (C-D), (A-D), and (A-C)).

```typescript
const graph = {
    'A': ['B', 'C', 'D'],
    'B': ['A', 'C'],
    'C': ['A', 'B', 'D'],
    'D': ['A', 'C'],
};

/*
  A --- B
  | \   |
  |  \  |
  |   \ |
  D --- C
*/
```

Hash tables handle sparse graphs in a particularly efficient way. Unlike an adjacency matrix representation of a graph, which requires space proportional to the square of the number of vertices, an adjacency list representation **only needs space proportional to the number of edges**. This is especially **beneficial when dealing with graphs where the number of edges is significantly less than the total possible edges**, thus **saving memory**.

### Memoization (Top-Down Dynamic Programming)

Hash tables are a key part of top-down dynamic programming, commonly referred to as [memoization](https://interviewing.io/memoization-interview-questions). [Dynamic programming](https://interviewing.io/dynamic-programming-interview-questions) is a technique used to solve complex problems by breaking them down into simpler sub-problems, solving each of those sub-problems just once, and storing their results for when the same sub-problem occurs again. This strategy of storing sub-problem solutions is known as memoization.

A hash table is a perfect data structure for implementing memoization due to its fast access times. It can store the results of sub-problems using problem parameters as keys. This is crucial for efficiency as it ensures that each sub-problem is computed only once, rather than repeatedly. When encountering a sub-problem, we first check the hash table to see if we've already calculated the result of this problem. If we find it, we use the stored result directly. If we don't find it, we solve the problem and store the result in the hash table. The key represents the current subproblem and the value represents the previously calculated subproblem's answer.

## Common Mistakes in Interviews Featuring Hash Tables

### Null keys in languages that don't support them

Picture this: you've got a huge, hungry dog (our hash table), and you're trying to feed it an invisible, scentless treat (a null key). That just won't work, right? The dog won't know what to do with it. That's pretty much what happens when you try to put a null key into a hash table in languages that don't support them.

**Many languages' hash tables don't support null keys because their hash functions don't know how to handle 'nothing'**. It's like trying to find a place in our car park for a car that doesn't exist. Things get messy, and you'll likely end up with an error, or worse, a program crash.

So, what's the big mistake here? Programmers sometimes forget to check for nulls or they assume that their hash table can handle null keys. It's like they're absent-mindedly trying to feed the dog that invisible treat, not realizing it won't work.

So remember, **before you try to add a key to your hash table**, **always make sure it's not null** (or that your hash table can handle it) to keep your program running smoothly.

### Trying to Hash Unhashable Objects

Another common mistake is trying to put a mutable object as the key for a hash table.

Python will throw a fit (a TypeError, to be exact) because lists are mutable, meaning they can be changed after they're created. Lists can't be hashed because who knows what they'll look like in the future?

In **JavaScript**, it's **technically allowed to use an array as a key in an object**, but it doesn't behave as you might expect. JavaScript **will convert the array to a string to use as a key**, and **changes to the array after the fact won't affect the object**.

Java allows you to use a list as a key in a map because Java lists are immutable, but changes to the list after it's been used as a key won't affect the map. This is because Java uses the original list's hashCode at the time it was inserted into the map, and that doesn't change if you assign a new list to the myList variable.

```typescript
let myList = [1, 2, 3];

// Try to use it as a key in an object (which is similar to a hash table in Python)
let myDict = {};
myDict[myList] = 'value';  // This will not raise an error!

console.log(myDict); // { '1,2,3': 'value' }

// However, it doesn't work like one might expect. Changing myList…
myList = [4, 5, 6];

console.log(myDict); // Still { '1,2,3': 'value' }
```

So, how do you get around it if you were looking to store a list as the key? In Python, one way is to use a tuple instead of a list if your data doesn't need to change. Tuples are immutable, meaning they can't be changed after they're created, so they're safe to hash:

```python
# Create a tuple
my_tuple = (1, 2, 3)

# Use it as a key in a dictionary
my_dict = {my_tuple: 'value'}  # This is fine!
```

If your language doesn't have tuples, another way to accomplish the same thing would be to sort the list and then convert the sorted list into a string. Be aware that this adds more time to your algorithm due to the O(N log N) sorting, but it can work in a pinch.

```typescript
// Create a list
let myList = [1, 2, 3];

// Sort the list and convert it to a string
let myKey = myList.sort().toString(); // "1,2,3"

// Use it as a key in an object
let myDict = {};
myDict[myKey] = 'value';  // This works!

console.log(myDict);  // Prints: { '1,2,3': 'value' }

// Now, create another list with the same values but in a different order
let myOtherList = [3, 2, 1];

// Sort this list and convert it to a string
let myOtherKey = myOtherList.sort().toString();

console.log(myOtherKey in myDict);  // Prints: true
```

In both JavaScript and Java, you can sort a list/array and then convert it to a string to use as a key in an object/map. You can then check if a key exists in the object/map. In JavaScript, you use `in`, and in Java, you use `containsKey()`. Note that Java's `List.sort()` modifies the list in place, so you need to sort a copy of the list if you want to keep the original list unchanged.

## What to Say in Interviews to Show Master Over Hash Tables

### Logically Walk Through Which Data Structure Should Be Used

It is the **sign of a senior engineer to not jump to conclusions**. **Avoid suggesting a hash table just because you need a constant time lookup**! You should **think out loud** and **come to the conclusion on whether or not a Set or even an Array could do the job before deciding on a hash table**.

- _"For this [Two Sum](https://interviewing.io/questions/two-sum) problem, it would be helpful to quickly look up the numbers I have access to. I don't just need to know the number though, I need a number and the location of what index the number was at. I can store this information in a hash table with the key as the number and the value as the index where that number was seen."_
- _"In my [DFS](https://interviewing.io/depth-first-search-interview-questions) I need to track every node I've visited previously. I could store it in a hash table with the key as the node and I could just set the value to 1 or true… but that's storing more information than I need. I guess I just need to track the key without a value so a set would be a better data structure here."_

### Discuss Hash Table Implementation Details When Appropriate

To show mastery of hash tables, **you should demonstrate knowledge of how they work under-the-hood and mention it organically**. There is a balancing act here – we don't want to go off on unnecessary tangents, but **providing extra details without taking extra time can give tremendously different impressions**. Imagine three candidates that all talk tell the interviewer about how they are going to use a hash table.

- _[**Junior**] "I'll use a hash table here": Not great. You've identified the data structure you might need, but haven't explained why it is a good choice._
- _[**Intermediate**] "I'll use a hash table here so we can leverage the constant time lookups": Better! Here we say what we are going to do, but also why we are doing it with a little implementation knowledge added._
- _[**Senior**] "I'll use a hash table here so we can leverage their **[[Amortized]] constant time lookups**": Stellar. Here you say what you're going to do, why you're going to do it, and demonstrate a deep understanding of hash tables under the hood with the key word "[[Amortized]]"_

The full implementation details of a hash table are too much to get into in this article, but you should be able to describe in detail how a hash table works. Here are some key words and concepts to review and consider adding to the conversation where appropriate.

- Review how **hash tables are just [Arrays](https://interviewing.io/arrays-interview-questions) under-the-hood**.
- Understand what **collisions** are and **why they are a problem**.
- Internalize strategies used to deal with collisions including: **linear probing**, **double-hashing**, **open-chaining**, and **quadratic hashing**.
- Review what makes a good **hash function**.
- Familiarize yourself with why lookups are **amortized** constant time, but occasionally are not due to the need to deal with collisions and also **rehashing** when we resize the hash table.

### Discuss Language-Specific Details to Show You Know Your Stuff

- **In Java, discuss which implementation to use**. As mentioned earlier, there are many key-value data structures available in Java, so being aware of all of them and their specific use-cases makes you look like a pro. Can you discuss the differences between HashMap, TreeMap, LinkedHashMap, and HashTable classes? If you can, this is a great signal for your interviewer.
- **In JavaScript, discuss the newer Map object**. Many developers still use JavaScript objects as hash tables for LeetCode-style problems. Highlighting your knowledge of the ES6 Map object shows you've worked in more modern JavaScript applications and aren't stuck in old JavaScript paradigms.
- **In C++, discuss `std::map` & `std::unordered_map` under-the-hood differences**. Many casual C++ users don't realize that `map` is implemented as a Red-Black tree in C++ not a hash table and therefore has logarithmic lookups – not constant time lookups! With `std::map` we get ordering guarantees at the cost of using more memory and slightly slower lookups. If you don't care about order and want faster access definitely use std::unordered_map and tell your interviewer why you chose it!
- **In Python, show technical depth by mentioning the `OrderedDict` in the `collections` module when appropriate**. It should be no shock that Python (which is built on C++) has its key-value container which is similar to C++'s `std::unordered_map`. `OrderedDict` is closer to C++'s `std::map` but still is implemented as a hash table (not a Red-Black tree). It has the useful extra guarantee of remembering the insertion order of elements. Python 3.7 introduced this guarantee into their standard dictionary implementation, but it is an implementation detail that is better not to rely on.