# Heap
```py
heap = []
heapify(heap)
```
## Min Heap
each internal node is smaller than or equal to its children
#### Use Cases
- Priority Queue
- Dijkstra Algorithm
- Sorting
- Median Finding

| Min Heap                                                                                                                    | Max Heap                                                                                                                       |
| --------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| In a Min Heap, the key present at the root node must be less than or equal to among the keys present at all of its children | In a Max Heap, the key present at the root node must be greater than or equal to among the keys present at all of its children |
| In a Min Heap, the minimum key element is present at the root                                                               | In a Max Heap, the maximum key element is present at the root                                                                  |
| A Min Heap uses the ascending priority                                                                                      | A Max Heap uses the descending priority                                                                                        |
| In a Min Heap, the smallest element is the first to be popped from the heap                                                 | In a Max Heap, the largest element is the first to be popped from the heap                                                     |
# HashMap
1. **Hashing**: The key in a HashMap is used to determine the index (position) where the corresponding value will be stored and retrieved. To do this, a hash function is applied to the key. The hash function computes a hash code, which is an integer that represents the key
2. **Bucket Array**: Internally, a HashMap is typically implemented as an array of "buckets". Each bucket can store multiple key-value pairs. The number of buckets is determined by the HashMap's capacity, which can be set when the HashMap is created
3. **Index Calculation**: To determine the index for a key-value pair, the hash code of the key is computed, then the modulo operation is applied to limit the index within the range of available buckets. The result of the modulo operation is the index where the pair will be stored
4. **Collision Handling**: Hash collisions occur when two different keys have the same hash code and map to the same bucket. HashMaps use a strategy called "chaining" to handle collisions. In a chained HashMap, each bucket can hold a linked list (or other data structure) of key-value pairs that have collided. When a collision occurs, the new key-value pair is simply appended to the linked list at the corresponding bucket
5. **Load Factor**: The load factor is a value between 0 and 1 that represents the ratio of the number of stored key-value pairs to the total number of buckets. When the load factor exceeds a certain threshold (usually around 0.75), the HashMap is resized (i.e., the number of buckets is increased), which helps maintain efficient performance
6. **Retrieval**: To retrieve the value associated with a key, the same hash code calculation is performed on the key to find the index of the bucket, and then a search is conducted within that bucket's linked list to find the specific key-value pair
## Java Specific Context & Implementation
`equals` is used to determine whether two objects are equal, while `hashCode` is used to calculate an integer value representing an object, primarily for efficient storage and retrieval in hash-based data structures. When you override `equals`, you should also override `hashCode` to ensure that equal objects have the same hash code, maintaining consistency for hash-based collections.
When you try to insert a new object into a `HashSet` in Java that has differing `equals` method but the same `hashCode`, you can end up with multiple objects in the `HashSet` that are considered unequal according to the `equals` method but are stored in the same bucket due to their identical hash codes This situation can lead to unexpected behaviour and violates the contract of `equals` and `hashCode`