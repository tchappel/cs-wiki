# Hashing

## Interface vs Implementation

The **interface** is the API, the contract that specifies how we can interact with the data structure.

The **implementation** is the code that actually makes the data structure work.

## Hash Map

Hash maps are a data structure that allows you to store key-value pairs, where each key is unique.

They are implemented combining an array with a hash function.

In the context of hash maps, a **hash function** takes an input (key) and deterministically converts it to an integer that is less than a fixed size (the size of the array).

- the key (which should be immutable) is converted into an index in the array where the value is stored.
- the hash function ensures that the same key always maps to the same index.
- if two keys map to the same index (**collision**), the hash map should use a technique to resolve it...

A hash map can add and remove elements in O(1), as well as update values associated with a key and check if a key exists, also in
O(1). You can iterate over both the keys and values of a hash map, but the iteration won't necessarily follow any order (there are many implementations vary and are language-dependent).

A hash map allows you to reduce the time complexity of an algorithm by a factor of O(n) for a huge amount of problems.

Every major language has a **built-in implementation** of a hash map:

- JavaScript: `Object` or a `Map`
- Python: `Dictionary`,
- Java: `HashMap`.

**Hash Map Interface (Javascript)**:

```javascript
// Declaration: use the Map object
let hashMap = new Map();

// If you want to initialize it with some key value pairs, use the following syntax:
let hashMap = new Map([
  [1, 2],
  [5, 3],
  [7, 2],
]);

// Checking if a key exists O(1)
hashMap.has(9); // false

// Accessing a value given a key O(1)
hashMap.get(5); // 3

// Adding or updating a key O(1)
// If the key already exists, the value will be updated
hashMap.set(5, 6);

// If the key doesn't exist yet, the key value pair will be inserted
hashMap.set(9, 15);

// Deleting a key O(1)
hashMap.delete(9);

// Get size O(1)
hashMap.size; // 3

// Iterate over the key value pairs O(n)
for (const [key, value] of hashMap) {
  console.log(key + " " + value);
}
```

## Set

A Set is a collection data structure that stores unique values—no duplicates allowed. If the same item is already inside, adding it again does nothing.

Like a hash map (hash table), a Set uses a hash function to convert each element into an integer index. However, unlike a hash map, it does not store key-value pairs—in a Set, the element itself is hashed and serves as the key.

Major languages **built-in implementations**:

- JavaScript: `Set`
