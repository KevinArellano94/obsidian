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

"**Open addressing**", on the other hand, is like the valet looking for the next available spot. If we are parking the cars right next to one another then that's "linear probing". If the valet starts hopping around in a specific pattern then it is quadratic probing or double hashing in the CS world.

Imagine our valet is having a bad day and just trying to park all the cars as close together in the same spot as possible, causing a traffic jam, or putting all the cars so far away it takes forever to get to them. This will result in a lot of collisions and will make a mess! That's like a poor hash function in coding. A good hash function, like a top-notch valet, parks the cars in a way that they're spread out evenly (avoiding traffic jams or "collisions") and are easy to retrieve when needed.

Now imagine that our parking lot is getting filled up. This is when "rehashing" comes in. It's like the valet suddenly puts in an order for a bigger parking lot, moves all the cars around to space them out more, reducing the chances of assigning two cars to the same spot.

Even though finding a parking spot (or an array index!) might sometimes take longer than expected, over many trips to the lot (or "amortized over time"), our valet (hash function) usually gets us there pretty quickly, averaging out to constant time. Here's a little python code as an example. The code supports a fixed size table of 10 elements and does not rehash when the table gets full and just continues to use separate chaining to avoid collisions (eventually degrading performance).