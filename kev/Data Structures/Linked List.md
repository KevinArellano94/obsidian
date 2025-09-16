---
tags:
  - linkedlist
  - datastructure
time complexity: O(n)
space complexity: O(1)
---
## What is a Linked List?

A linked list is a data structure consisting of a **sequence of nodes**, where each node contains a reference to either the next node in the sequence, itself, or the node prior to it. They are designed to be **efficient when** performing **insertions** and **deletions**. The key to their efficiency as we will discuss further is the use of pointers to capture the order of the nodes.

Linked lists come in different variations such as **singly linked** (nodes only point to the next node or the previous node in a reverse linked list), **doubly linked**, **self-linked lists**, and **circular linked lists**.

### Types of Linked Lists

Singly and doubly linked lists are the two major types based on the direction of linkage. That said, we will also expand on circular linked lists and self-linked lists. This is because they tend to be a major source of headaches when implementing Linked Lists thus understanding their properties will help avoid these pitfalls.

- 1. Singly-linked lists: each node **has a link to the next node** in the list, but **not to the previous node**.
- Doubly linked lists: each node has **links to both the next node and the previous node** in the list.
- Circular linked lists: the **last node in the list points to the first node**, creating a circular structure. This **allows for efficient traversal of the list in both directions**.
- Self-referential linked lists or self-linked lists: **each node contains a pointer or reference to itself**. This type of linked list is not commonly used in practice but can be used in certain specialized scenarios such as **implementing circular queues** or **resolving collisions** by chaining in hashmaps.

### Common Operations on Linked Lists

To effectively understand when to use a linked list, it helps to understand how we use them first.

#### Linked List Traversal

Here is some pseudocode for forward and backward traversals of a linked list:

##### Forward Traversal

Both doubly and singly linked lists allow for a simple forward traversal. Do note the None check.

#### Code example

```typescript
export class Node<T> {
    constructor(
        public value: T | null = null,
        public nextValue: Node<T> | null = null,
        public previousValue: Node<T> | null = null,
    ) {}
}
  
if (import.meta.main) {
    // Create a sample doubly linked list
    // For demo: head -> 1 <-> 2 <-> 3 <- tail
    const node1 = new Node<number>(1);
    const node2 = new Node<number>(2);
    const node3 = new Node<number>(3);
  
    node1.nextValue = node2;
    node2.previousValue = node1;
    node2.nextValue = node3;
    node3.previousValue = node2;
  
    const head = node1;
    const tail = node3;
  
     // Forward traversal
    console.log("Forward traversal (from head):");
    let currentNode: Node<number> | null = head;
    while (currentNode !== null) {
        // Do something with the current node, e.g., log its value
        console.log(currentNode.value);
        currentNode = currentNode.nextValue;
    }
  
    // Reverse traversal
    console.log("Reverse traversal (from tail):");
    currentNode = tail;
    while (currentNode !== null) {
        // Do something with the current node, e.g., log its value
        console.log(currentNode.value);
        currentNode = currentNode.previousValue;
    }
}
```

#### Insertion Into a Singly Linked List

The process for inserting an element into a singly linked list is as follows:

1. **Create a new node** containing the value to be inserted.
2. **Determine the position** where the new node will be inserted.
3. If the insertion **position is at the front of the list**, set the next in the **new node to the current head** of the list.
4. If the insertion **position is somewhere in the middle of the list**, **find the node immediately preceding (prev)** the position where the new node will be inserted. You can determine this by simply checking if the next node is in the position you want to insert. **Your current node thus becomes your preceding node** and the **node following it becomes the previous next node**.
5. **Update the link in the preceding node** to point to the new node.
6. **Update the link in the new node to point** to the node that was previously at the insertion position (The previous next node).
7. If the insertion **position is at the end of the list**, set the link in the **preceding node to the new node**, and set the link in the **new node to None**.

Insertions into **doubly-linked lists would entail also updating the previous pointer of the new node to the preceding node** and the **previous of the next node to the new node** in addition to the **updates required for inserting into a singly** linked list.

##### Head Insertion

Simply set the new node’s next pointer to the current head. In case the **list is empty**, the **new node becomes the head and tail**, with its **next pointing to None**.

##### Insertions into the Middle

These usually entail **slicing the linked list** and then **setting pointers to the new node in preceding nodes** and from the new node to the next nodes. The reverse also applies for doubly linked lists.

![[Pasted image 20250913141114.png]]

##### Tail Insertion

Point the **next pointer of the last node to the new node**, and point the **new node to None**.

The time complexity for inserting an element in a singly linked list is **`O(n)`** in the worst-case scenario, where n is the number of nodes in the list. This is because finding the node immediately preceding the insertion position **requires traversing the list**, which can take up to **`O(n)` time**. The **space complexity** of inserting a new node into a singly linked list is **`O(1)`**, as **only one new node is created** and **no additional memory is allocated**.

#### Deletion from a Singly Linked List

The process for deleting an element from a singly linked list is as follows:

1. **Find the node** to be deleted. **If they exist**, Keep **track of the node pointing to it (preceding node)** and the **node immediately following the node we are deleting (next node)**.
2. If the node to be deleted is the **head of the list**, **update the head to the next node of the head**.
3. If the node to be deleted is in the **middle of the list**, point the preceding node link to the next node link, **bypassing the node to be deleted**.
4. Update the link in the preceding node to point to the node immediately following the node to be deleted.
5. If the node to be deleted is the **tail of the list**, update the link in the preceding node to **point to None**.

The time complexity for deleting an element from a singly linked list is also **`O(n)`** in the worst-case scenario, where n is the number of nodes in the list. This is because finding the node immediately preceding the deletion position requires traversing the list, which can take up to **`O(n)` time**. The **space complexity** is also `O(1)`.

##### Head Deletion

Make the **new head the next node of the current head**. This **could be a node** or **None**

##### Deletions in the Middle

[duplicate image from above]

[[Drawing 2025-09-13 14.26.44.excalidraw]]

![[Pasted image 20250913142746.png]]

Make the next of the second to the last node point to the previous node.  

##### Tail Deletion

Make the **next of the second to last node point to None** (**Bypass the last non-None node**)

#### Insertion into Doubly Linked Lists

Inserting an element into a doubly linked list is **similar to inserting an element into a singly linked list**, only that the operations done to point next have to be **repeated from the opposite direction**. The following steps break down how we achieve this.

1. Create a new node containing the value to be inserted.
2. Determine the position where the new node will be inserted.
3. If the insertion position is at the front of the list, set the next in the new node to the current head of the list, and set the previous node’s next pointer to the new node.
4. If the insertion position is somewhere in the middle of the list, find the node immediately preceding the position where the new node will be inserted. You can determine this by simply checking if the next node is in the position you want to insert. Your **current node** thus becomes your **preceding node** and the node following it becomes the **previous next** node.
5. Update the **next** link in the preceding node to point to the **new node**.
6. Update the **previous** link in the **new node** to point to the **preceding node**.
7. Update the **previous** link in the **previous next** node to point to the **new node**.
8. Update the **next** link in the **new node** to point to the **previous next** node.

Similar to the singly linked list case, the time **complexity for insertions is `O(n)`** in the worst-case scenario. This is because finding the node immediately preceding the insertion position requires traversing the list, which can take up to `O(n)` time. The space complexity of inserting a new node into a doubly linked list is still `O(1)`.

#### Deletion from a Doubly Linked List

Deletion is a bit more straightforward.

1. Find the node to be deleted. Take note of the node preceding it and the node following it.
2. If the node to be deleted is the head of the list, update the head to the next node of the head, and set the previous link in the new head to None.
3. If the node to be deleted is in the middle of the list, update the **next** link in the **preceding node** to point to the **next node** (bypassing the node to be deleted).
4. Update the **previous** link in the **next node** to point to the **preceding node**.
5. If the node to be deleted is the tail of the list, update the previous link in the preceding node to point to None.

The time complexity and space complexity for this operation is also `O(n)` and `O(1)` respectively. This is again due to the traversal needed to locate the node we want to delete.

#### Insertions and Deletions into Circular and Self-Linked Lists

These flavors will usually have linkage styles resembling either a singly or doubly linked list. In the case of circularly linked lists, the process resembles breaking, shortening, and reconnecting a chain. One note is that linear but self linked lists have the cycle occuring anywhere along the linked list. Circular linked lists will have the tail of the linked list point to the head. A special case is a single node, circular linked list which also can be considered a self linked list. The steps remain the same as above depending on the linking logic in the nodes affected.

#### Code example:

```typescript
export class Node<T> {
    data: T;
    previous: Node<T> | null;
    next: Node<T> | null;
  
    constructor(data: T) {
        this.data = data;
        this.next = null;
        this.previous = null;
    }
}
  
export class DoublyLinkedList<T> {
    head: Node<T> | null;
    tail: Node<T> | null;
    length: number;
  
    constructor(data: T) {
        this.head = null;
        this.tail = null;
        this.length = 0;
        if (data !== undefined) {
            const headNode = new Node(data);
            this.head = headNode;
            this.tail = headNode;
            this.length = 1
        }
    }
  
    isEmpty(): boolean {
        return this.head === null;
    }
  
    add(data: T): void {
        this.addNode(data);
    }
  
    private addNode(data: T) {
        const newNode = new Node(data);
        if (this.isEmpty()) {
            this.head = newNode;
            this.tail = newNode;
        }
        else {
            if (this.tail !== null) {
                this.tail.next = newNode;
                newNode.previous = this.tail;
                this.tail = newNode;
            }
        }
        this.length++;
    }
  
    addFirst(data: T): void {
        this.addFirstNode(data);
    }
  
    private addFirstNode(data: T) {
        const newNode = new Node(data); // Fresh node: { data, previous: null, next: null }
        if (this.isEmpty()) {
            // Empty list: New node becomes both head and tail (single-node list).
            this.head = newNode;
            this.tail = newNode;
        } else {
            if (this.head !== null) {
                // Step 1: Old head is no longer the front—link its previous to the new node
                // (Creates backward traversal: old head can now go "prev" to new node)
                this.head.previous = newNode;
  
                // Step 2: New node's next points to old head
                // (Creates forward chain: new node → old head)
                newNode.next = this.head;
  
                // Step 3: Update the list's entry point to the new node
                // (Now traversal starts here; tail unchanged)
                this.head = newNode;
            }
        }
        this.length++;
    }
  
    addAt(data: T, index: number): void {
        if (index < 0 || index > this.length) throw "Illegal argument";
        if (index === 0) this.addFirst(data);
        else if (index === this.length) this.addNode(data);
        else {
            if (index < this.length / 2) {
                let currentNode: Node<T> | null = this.head;
                for (let i = 0; i < index; i++) {
                    if (currentNode !== null) {
                        currentNode = currentNode.next;
                    }
                }
                if (currentNode !== null) {
                    this.newNodeAssignment(currentNode, data);
                }
            } else {
                let currentNode: Node<T> | null = this.tail;
                for (let i = this.length - 1; i > index; i--) {
                    if (currentNode !== null) {
                        currentNode = currentNode.previous;
                    }
                }
                if (currentNode !== null) {
                    this.newNodeAssignment(currentNode, data);
                }
            }
        }
    }
  
    private newNodeAssignment(currentNode: Node<T>, data: T): Node<T> {
        const newNode = new Node(data);
  
        if (currentNode.previous !== null) {
            currentNode.previous.next = newNode;
        }
        newNode.previous = currentNode.previous;
        newNode.next = currentNode;
        currentNode.previous = newNode;
        this.length++;
  
        return newNode.next;
    }
  
    deleteFirst(): void {
        this.deleteFirstNode();
    }
  
    private deleteFirstNode(): void {
        if (this.isEmpty()) throw "LinkedList is empty, there are no items to delete";
  
        if (this.head !== null) {
            const data: T = this.head.data;
  
            this.head = this.head.next;
            this.length--;
        }
    }
  
    deleteLast(): void {
        this.deleteLastNode();
    }
  
    private deleteLastNode(): void {
        if (this.isEmpty()) throw "LinkedList is empty, there are no items to delete";
  
        if (this.tail !== null) {
            const data: T = this.tail.data;
  
            this.tail = this.tail.previous;
            this.length--;
        }
  
        if (this.isEmpty()) this.head = null;
        else {
            if (this.tail !== null) {
                this.tail.next = null;
            }
        }
    }
  
    deleteAt(index: number): void {
        if (index < 0 || index > this.length) throw "Illegal argument";
        if (index === 0) this.deleteFirst();
        else if (index === this.length - 1) this.deleteLast();
        else {
            if (index < this.length / 2) {
                let currentNode: Node<T> | null = this.head;
                for (let i = 0; i < index; i++) {
                    if (currentNode !== null) {
                        currentNode = currentNode.next;
                    }
                }
                if (currentNode !== null) {
                    this.deleteAtNode(currentNode);
                }
            } else {
                let currentNode: Node<T> | null = this.tail;
                for (let i = this.length - 1; i > index; i--) {
                    if (currentNode !== null) {
                        currentNode = currentNode.previous;
                    }
                }
                if (currentNode !== null) {
                    this.deleteAtNode(currentNode);
                }
            }
        }
    }
  
    private deleteAtNode(node: Node<T>): void {
        // Unlink: Connect previous to next, and next to previous
        if (node.previous !== null) {
            node.previous.next = node.next;
        }
        if (node.next !== null) {
            node.next.previous = node.previous;
        }
  
        // Update head/tail if deleting the endpoint nodes (robust, even if deleteAt routes them)
        if (this.head === node) {
            this.head = node.next;
            if (this.head !== null) {
                this.head.previous = null;
            } else {
                this.tail = null;  // List now empty
            }
        }
        if (this.tail === node) {
            this.tail = node.previous;
            if (this.tail !== null) {
                this.tail.next = null;
            } else {
                this.head = null;  // List now empty
            }
        }
  
        this.length--;
  
        // Clean up the node (prevents memory leaks in non-GC environments; optional in JS/TS)
        node.data = null as any;  // Type assertion since T might not be null
        node.next = null;
        node.previous = null;
    }
  
    toString(): string {
        const values: string[] = [];
        let current = this.head;
        while (current) {
            values.push(current.data.toString());
            current = current.next;
        }
        return values.join(' <-> ');
    }
}  

if (import.meta.main) {
    const dll = new DoublyLinkedList('One');
    // Example: Add more items
    dll.add('Two');
    dll.add('Four');
  
    // Example: Add to first
    dll.addFirst('zero');
  
    // Example: Add at this index
    dll.addAt('Three', 3);
    dll.addAt('10', 5);
    
    // Example: Delete first item
    dll.deleteFirst();
  
    // Example: Delete last item
    dll.deleteLast();
  
    // Example: Delete at index
    dll.deleteAt(2);
  
    console.log(dll.toString());  // Output: One <-> Two <-> Three
    console.log('Length:', dll.length);  // Output: Length: 3
}
```

#### Array Implementation

Linked lists can be implemented using [arrays](https://interviewing.io/arrays-interview-questions), where each element of the array represents a node in the linked list. Every element contains a value and a link to the next node in the list, represented by the index of the next element in the array. The last element in the array contains a special value, usually None, to indicate the end of the list. For example, consider the following array:

```css
[(2, 1), (5, 2), (7, 3), (4, None)]
```

In the above, the head is the first element, with the tuple representing the value as well as the next node’s index. The corresponding linked list would be as follows:

```rust
2 -> 5 -> 7 -> 4 -> None
```

Linked lists implemented with arrays have some advantages over traditionally implemented ones, such as better cache locality and the ability to preallocate memory. Array gives an additional benefit of constant time access to its element if the index is already known. This can speed up the retrieval of a node's value if its index in the array is already known. They come with some cons though, such as the need to allocate a fixed amount of memory, which can lead to wasted space or insufficient space for large lists, and the need to update links in the surrounding nodes as the pointers reference specific indices in the array. This shifting around means that the Insertion complexity is `O(n)`, in addition to the traversal cost. It doesn't really change the overall complexity in this regard, but it is less efficient.

#### Hashmap Implementation

Given the implementation above using arrays, we can see how the hashmap implementation would work. Simply put, the representation for the above example would be as follows:

```css
 { 
   0: {'value': 2, 'next': 1}, 
   1: {'value': 5, 'next': 2}, 
   2: {'value': 7, 'next': 3}, 
   3: {'value': 4, 'next': None} 
 }
```

The rest of the logic remains the same.

Do note, in some cases, an array itself can be used to represent the pointers. This is a key insight to solve questions such as the [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/) problem.

The values are not taken into account in the array representation, but noting them is as simple as using the tuple notation above or maintaining a separate list with the values ordered by the indices.

#### Inbuilt Types

In some languages like Java and C++, LinkedLists are offered out of the box as part of the language. Here are examples in [Java](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html) and [C++](https://cplusplus.com/reference/list/list/).

## When to Use Linked Lists in Interviews

1. **Implementing a [stack](https://interviewing.io/stacks-interview-questions) or [queue](https://interviewing.io/queue-interview-questions) data structure**. Stacks and queues only add or remove from the ends, this can be achieved in a linked list the same way by adding or removing nodes from the head or tail of the list. **A simple array-based implementation would suffice for this as we would be popping or appending to the array at the head or tail, but with constant time operations**. Keep in mind, Appending an element at the beginning of the array (e.g. .shift() in JS) **could be a costly O(n) operation as it requires shifting of all the array elements**. As a result, array-based implementation for a queue could be costly. **Linked List mitigates that cost**.
2. **Maintaining a sorted list of values**. In this case, we can maintain a sorted list of values by inserting nodes in the correct position based on their value. With an **array based implementation**, **searching for the position to insert nodes can be done in logarithmic time using binary search** which improves the efficiency further. A **Linked Hashmap implementation (See appendix) would be useful in this case**.
3. **Implementing a [hash table](https://interviewing.io/hash-tables-interview-questions)**. We can implement a hash table by **storing key-value pairs in nodes** and using a **hash function to determine the index of the linked list** where the **node** should be stored with colliding nodes all pointing to the same index.
4. Implementing a [graph data structure](https://interviewing.io/graphs-interview-questions). Fundamentally, **linked lists are unary trees/ graphs**.
5. **Implementing a [priority queue](https://interviewing.io/queue-interview-questions)**. Linked lists are most commonly used to **implement priority queues** by **maintaining the list in sorted order based on priority and inserting** new nodes in the correct position. This is owing to the ease and efficiency of insertions and deletions.
## Common Interview Mistakes Featuring Linked Lists

1. **Not knowing how to traverse the list**. a. It is key to know which direction, forward (to next node) or backward (to previous node) traversal. b. Check for **None** before trying to access the next or previous nodes. Interviewees often fail to account for the tail node being None. They thus try to perform node operations the same way they would with non-None nodes.
2. **Not using a dummy node when traversing or performing insertions and deletions**. See the dummy nodes section below to see how dummy nodes can simplify the code.
3. **Infinite loops with circular linked lists or self-linked lists**. These occur when nodes self-reference or we have a circular linked list. **Caching seen nodes** or using **Floyd’s algorithm (Tortoise and Hare)** can be useful for cycle detection. We go into detail on the algorithm in the mastery section.
4. **Overly complicated implementation**. Most people know to use nodes and pointers. However, most linked lists are usually simple enough to be implemented using an array or a hashmap.
5. **Complexity analysis fails to account for traversal**. The advantages of linked lists are many, including **efficient insertions** and **deletions** that have a **reference to the location**. However, finding the correct position for these operations, or **searching for a specific node, can be costly as it requires traversing the list**. When doing complexity analysis, it is key to account for this when doing the overall performance analysis. That said, the hashmap approach to implementation can help resolve the search inefficiency.
6. **Confusion with the insertion and deletion steps**. We go into extensive detail on this above.
7. **Failing to account for edge cases eg. insertions to the head or tail of the linked list**. Head and Tail insertions tend to be the most common insertion and deletion operations hence why it is important to remember how to deal with them.

## Clarifying Questions to Ask Your Interviewer About Linked Lists

1. **What operations do we need to perform?** If the core focus is the linked list implementation, otherwise infer from the case study and list these.
2. **Do we have a defined node structure?** If the class format is provided, implement a traditional linked list. If the case is simple enough, a hashmap or array may suffice.
3. **Is the linked list singly linked or doubly linked?** Clarify this. Don't be afraid to use a doubly linked list for the efficiency gains traversing forward and backward. If memory is not a constraint, see if you can use the Linked Hashmap implementation.
4. **Is there a limit to the size of the linked list?** This can be an issue especially if we are dealing with data streams. It may be easier and more efficient to use arrays or hashmaps with very large linked lists. Arrays are usually native (complex) data structures in most languages and thus are usually efficient to manipulate at scale.
5. **Do we want to account for the traversal complexity when doing the complexity analysis?** This is key as it shows mindfulness of an operation that overhauls a lot of the efficiency gains when using linked lists.

## How to Show Mastery of Linked Lists in Interviews

### Using a Dummy Node

Using a dummy node/ sentinel node in a linked list can simplify the code by eliminating the need to handle the edge case where the list is empty or the node to be deleted is the head of the list separately. This can make the code cleaner and easier to understand, and can also help to avoid bugs that may arise from handling edge cases inconsistently. However, using a dummy node does come with some overhead, as an extra node must be allocated and maintained. Whether or not to use a dummy node depends on the specific requirements of the application and the personal preference of the developer.

In the below example, we insert a node at the beginning of a linked list with a dummy node:

```python
class Node:
    def __init__(self, data=None, next=None):
        self.data = data
        self.next = next

class LinkedList:
    def __init__(self):
        self.head = Node()

    def insert_at_beginning(self, data):
        new_node = Node(data, self.head.next)
        self.head.next = new_node
```

And here's an example of inserting a node at the beginning of a linked list without a dummy node, where we have to handle the edge case where the list is empty separately:

```python
class Node:
    def __init__(self, data=None, next=None):
        self.data = data
        self.next = next

class LinkedList:
    def __init__(self):
        self.head = None

    def insert_at_beginning(self, data):
        if self.head is None:
            self.head = Node(data, None)
        else:
            new_node = Node(data, self.head)
            self.head = new_node
```

As you can see, using a dummy node simplifies the code by eliminating the need to handle the edge case where the list is empty separately.

Similarly, to deleting a node from a linked list with a dummy node:

```python
class Node:
    def __init__(self, data=None, next=None):
        self.data = data
        self.next = next

class LinkedList:
    def __init__(self):
        self.head = Node()

    def delete_node(self, data):
        current_node = self.head
        while current_node.next is not None:
            if current_node.next.data == data:
                current_node.next = current_node.next.next
                return
            current_node = current_node.next
```

And here's a similar example without the dummy node:

```python
class Node:
    def __init__(self, data=None, next=None):
        self.data = data
        self.next = next

class LinkedList:
    def __init__(self):
        self.head = None

    def delete_node(self, data):
        if self.head is None:
            return

        if self.head.data == data:
            self.head = self.head.next
            return

        current_node = self.head
        while current_node.next is not None:
            if current_node.next.data == data:
                current_node.next = current_node.next.next
                return
            current_node = current_node.next
```

Again, using a dummy node simplifies the code by eliminating the need to handle the edge case where the node to be deleted is the head of the list separately.

### Linked HashMap

Further reading [here](https://docs.oracle.com/javase/8/docs/api/index.html?java/util/LinkedHashMap.html).

We can take advantage of the **O(1) lookup time hashmaps offer to efficiently implement LinkedLists**. This can come in handy when tackling problems such as LRU cache where the order of insertion is not guaranteed to be sorted thus we need to constantly look back at the cache to update the frequency of occurrence of entries or update the next and previous pointers. Take note of the previous and next nodes alongside each current node. This is memory inefficient of course as it needs a separate structure but it only scales out the total space complexity linearly thus the space complexity overall does not change while guaranteeing `O(1)` insertions and deletions. This implementation would look as follows:

```python
linked_map = {
	cur_node: <prev_node, next_node>
	prev_node: ...
	next-node: ...
}
```

### Floyd’s Algorithm (Tortoise and Hare)

Floyd's algorithm is a heuristic algorithm that detects the presence of a cycle in a linked list and returns the starting node of the cycle. The algorithm works by using [two pointers](https://interviewing.io/two-pointers-interview-questions), one that moves at a slower pace (the tortoise) and one that moves at a faster pace (the hare), to traverse the linked list.

This algorithm takes advantage of the concept of overlapping. On a circular race track, should one vehicle/ racer be faster, they will eventually overlap the slower racers as they continuously put some distance between them and the competitors. Similarly, when traversing linked lists that have cycles, if we have two pointers with one being faster (typically twice the speed of the slower pointer), then they will eventually converge somewhere along the cycle.

Assuming that the linked list has a cycle, the hare pointer will eventually catch up to the tortoise pointer and they will meet at a point in the cycle, which we will refer to as the meeting point. The distance traveled by the hare pointer will be twice the distance traveled by the tortoise pointer at the **meeting point**, since the hare moves twice as fast as the tortoise.

Now let's consider the distance between the head of the linked list and the starting point of the cycle, which we will refer to as the loop start. Let this distance be denoted as "x", and let the length of the cycle be denoted as "y". We can express the distance traveled by the hare and tortoise pointers in terms of "x" and "y" as follows:

- Distance traveled by tortoise pointer = x + m * y (where m is an integer representing the number of complete cycles made by the pointer)
- Distance traveled by hare pointer = x + n * y (where n is an integer representing the number of complete cycles made by the pointer)

Since the hare pointer moves twice as fast as the tortoise pointer, we can express the distance traveled by the hare pointer as twice the distance traveled by the tortoise pointer:

```css
2 * (x + m * y) = x + n * y
```

Simplifying this expression, we get:

```scss
x = (n - 2m) * y
```

This equation tells us that the distance between the head of the linked list and the loop start is a multiple of the length of the cycle. If we reset the tortoise pointer to the head of the linked list and move both pointers at the same pace, the distance between the head of the linked list and the loop start will be equal to the distance between the meeting point and the loop start. Therefore, if we move the tortoise pointer and hare pointer at the same pace until they meet again, they will meet at the loop start. In conclusion, Floyd's algorithm will usually find the start of the linked list cycle because it takes advantage of the fact that the distance between the head of the linked list and the loop start is a multiple of the length of the cycle, and uses this fact to determine the location of the loop start.

```python
# define a Node class
class Node:
    def __init__(self, val):
        self.val = val
        self.next = None

# define a function to detect cycles in a linked list
def detect_cycle(head):
    # initialize pointers
    slow = head
    fast = head

    # move pointers through linked list
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next

        # check for cycle
        if slow == fast:
            # reset slow pointer
            slow = head

            # move pointers until they meet again
            while slow != fast:
                slow = slow.next
                fast = fast.next

            # return starting node of cycle
            return slow

    # return None if no cycle is detected
    return None
```