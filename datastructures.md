# Data Structures

## SSTable

Sorted String Table

## MemTable

A sorted/balanced tree structure stored in memory, typically used for writes in a 
system that later saves the memtable to disk as a read-only SSTable.

## LSM Tree

Log Structured Merge Trees. Leveled structure for high performance indices - top level is 
for recently written data and kept in memory. As the in-memory structure grows and exceeds
a threshold the in memory portion is written to disk or merged with the on-disk level below it.

## Bloom Filter

In memory data structure that approximates the answer of membership in a set.
* When adding a value to a set, hash the value to an index in an array. Set the bit at that position to 1.
* To check for membership in the set, hash the value to the index and check the bit value:
  * If the value is 0 the item is guaranteed not to be in the set.
  * If the value is 1 the item *might* be in the set - due to indexing collisions.
* The value in the bloom filter is that it can avoid unnecessary reads when we get the guaranteed "not in set" answers.
