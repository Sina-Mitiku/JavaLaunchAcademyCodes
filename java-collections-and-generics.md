# Collections and Generics

---

## The Collection Interface

<img width="800" src="https://dzone.com/storage/temp/1821372-class-and-interface-hierarchy.png" alt="Collection Framework">

---

## Wait, What's an Interface?

- Remember inheritance? It's **kind of** like that
- An interface defines a set of methods that a given class **must** implement
- No implementation is included
- Each class that implements the methods fill in the blanks

---

## Collections

- To implement a `Collection` class, you need:
  - `contains(Object o)`
  - `equals(Object o)`
  - `isEmpty()`
  - `add(E e)`
  - `clear()`
  - `remove(Object o)`

...As well as some additional methods

---

## A Review of the Collections Framework

- Abstraction - representing a _bag_ where we group data together
- Every collection implementer will have methods to read, write, and traverse what's there
- Choose the right data structure for the use case

---

## Lists

- What we most commonly know as **Arrays**
- Data can be duplicated
- The order matters
- Implementers: `ArrayList`, `LinkedList`

---

## Queues

- Show the front of the list
- Traversal may not be guaranteed to be in order, depending on the class
- Implementers: `LinkedList`, `PriorityQueue`

---

## Queues

- Think of a line at the bank - all we care about is who's in front of the line
- First in, first out
- We can derive who's behind that person when they step up to the teller window
- Reading and Writing is less expensive
- We can traverse / iterate but it's more expensive

---

## E.g., a LinkedList

![Linked List Order Diagram][linked_list_order_diagram]
![Linked List Structure][linked_list_structure_image]

---

## Queue Methods

- `poll()` - retrieves and removes the head of the queue, returns `null` if empty
- `remove()` - retrieves and removes the head of the queue, throws exception if empty
- `peek()` - retrieves, but does not remove the head of the queue
- `element()` - retrieves, but does not remove the head, throws exception if empty

---

## Set

- No duplicates
- Can only have one `null` element
- Most commonly used implementer: `HashSet`

---

## HashMap

- `HashMap` is not part of the collection hierarchy
- It implements a `Map`
- It has collection-like behaviors, but does not directly implement the interface

---

## HashSet Example

```java
HashSet phoneNumbers = new HashSet();
phoneNumbers.add("8675309");
phoneNumbers.add("5551234");
phoneNumbers.add("5551234");
System.out.println(phoneNumbers.size());
```

---

What will this output?

## HashMap Example

```java
HashMap contacts = new HashMap();
contacts.put("Jenny", "8675309");
System.out.println(contacts.get("Jenny"));
```

---

## HashSet vs. HashMap

- `HashSet` does not have the idea of key,value pairs
- `HashSet` just stores values, does not care about order

- `HashMap` correlates keys to values

---

## Ok, so which one do I use?

- Do you need to correlate keys and values? Use a `HashMap`
- Do you need ensure elements are unique? Use an implementer of `Set`
- How volatile is the list?
  - If it's large and volatile, and you're mainly accessing or back of the list, use `LinkedList`
  - Otherwise, use `ArrayList`

This can be overwhelming - programming to **interfaces** can help (more on this later)

---

## A Helpful Graphic

[StackOverflow Post][collection-decision-tree]

---

## Generics

---

## Statically Typed Languages and Collections

- How do we know the data type of Collection elements?
- We can explicitly cast:

```java
List list = new ArrayList();
list.add("Sam");
list.add("Sally");

System.out.println((String)list.get(1));
```

---

## Problems with Explicit Casting

- Not restrictive on insertion
- Prone to bugs when collections contain multiple data types

---

## We can Provide Type Hints for Elements

```java
List<String> list = new ArrayList<String>();
list.add("Sam");
list.add("Sally");

System.out.println(list.get(1));
```

- Defined a **generic**
- Generics are identifiable with the `<>` **diamond** operator
- Introduced in Java 5

---

## Benefits of Generics

- Compile-time errors
- Strict type-checking on insertion
- Creates a **homogenous** selection
- Implicit casting when accessing elements

---

## HashMap usage of Generics - an Improvement

```java
HashMap<String, String> contacts = new HashMap<String,String>();
contacts.put("Jenny", "8675309");
System.out.println(contacts.get("Jenny"));
```

By properly using a generic, we can always assume a `String` key and a `String` value.

---

## Programming to Interfaces

- Assign to Interface instances to provide more future flexibility

```java
List<String> list = new ArrayList<String>();
```

---

## Map Implementers

- Just like `List` implementations, we have `Map` design options
- If we start to care about order, we use a `TreeMap`
- `LinkedHashMap` are great for cache stores - Least Recently Used (LRU) ordering
- `HashMap` usage is most common

---

## HashMap Improvement

```java
Map<String, String> contacts = new HashMap<String,String>();
contacts.put("Jenny", "8675309");
System.out.println(contacts.get("Jenny"));
```

- Programming to an interface allows us to use a different implementer of `Map`

[collection-decision-tree]: https://stackoverflow.com/questions/21974361/which-java-collection-should-i-use
[linked_list_order_diagram]: https://s3.amazonaws.com/horizon-production/images/article/java-linkedlist/linked_list_order_diagram.png
[linked_list_structure_image]: https://s3.amazonaws.com/horizon-production/images/article/java-linkedlist/linked_list_structure.png