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
