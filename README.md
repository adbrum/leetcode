# LeetCode Problem-Solving Patterns

This repository contains a **collection of the most common patterns** used to solve LeetCode problems efficiently.  
Each pattern includes:
- When to use it
- A representative problem
- Input/Output example
- An optimized Python solution (best possible **time/space complexity**)
- Step-by-step explanation of the approach

---

## 📚 Patterns Index

| #  | Pattern | Typical Use Case | Example Problem |
|----|---------|------------------|-----------------|
| 1  | [Two Pointers](#1-two-pointers) | Sorted arrays, palindromes, target sums | Two Sum II |
| 2  | [Sliding Window](#2-sliding-window) | Subarrays/substrings with constraints | Longest Substring Without Repeating Characters |
| 3  | [Fast & Slow Pointers](#3-fast--slow-pointers-floyds-cycle) | Detect cycles, find middle node | Linked List Cycle II |
| 4  | [Binary Search](#4-binary-search) | Sorted arrays, monotonic conditions | Find First and Last Position of Element |
| 5  | [Backtracking / DFS](#5-backtracking--dfs) | Subsets, permutations, combinations | Subsets |
| 6  | [Breadth-First Search (BFS)](#6-bfs-breadth-first-search) | Level-order traversal, shortest paths | Binary Tree Level Order Traversal |
| 7  | [Dynamic Programming (DP)](#7-dynamic-programming-programação-dinâmica) | Optimization with overlapping subproblems | House Robber |
| 8  | [Hash Tables](#8-hash-table-dicionários--mapas) | Fast lookup, complement check | Two Sum |
| 9  | [Monotonic Stack](#9-stack--monotonic-stack) | Next greater/smaller elements | Daily Temperatures |
| 10 | [Heap / Priority Queue](#10-heap--priority-queue) | Top-k, merging sorted lists | Kth Largest Element |
| 11 | [Union-Find (DSU)](#11-union-find--disjoint-set-dsu) | Connected components, cycle detection | Connected Components in Graph |
| 12 | [Trie (Prefix Tree)](#12-trie-prefix-tree) | Prefix search, autocomplete | Implement Trie |
| 13 | [Bit Manipulation](#13-bit-manipulation-operações-bitwise) | Unique elements, subset states | Single Number |

---

## 🚀 Example: Two Pointers

**Problem:** Two Sum II (input sorted)  
- **Input:** `numbers = [2,7,11,15], target = 9`  
- **Output:** `[1,2]` (1-based indices)

```python
def two_sum_sorted(numbers, target):
    l, r = 0, len(numbers) - 1
    while l < r:
        s = numbers[l] + numbers[r]
        if s == target:
            return [l+1, r+1]
        if s < target:
            l += 1
        else:
            r -= 1
    return [-1, -1]

- **Time Complexity:** `O(n)`  
- **Space Complexity:** `O(1)`

### Step-by-step
1. Start with two pointers (`l` at beginning, `r` at end).
2. Check the sum:
   - If equal → return indices.  
   - If less → move `l` right.  
   - If greater → move `r` left.  
3. Continue until they meet.

---

## 🧩 Other Patterns

Each pattern in this repo follows the same structure:
- **When to use**
- **Problem statement with I/O**
- **Optimized Python code**
- **Complexity analysis**
- **Step-by-step explanation**

---

## 🏆 Goal

The goal of this repository is to:
- Provide a **practical reference** for mastering LeetCode patterns.
- Help developers **recognize problem types** quickly.
- Offer **clean, optimized Python implementations**.

---

## 💡 Contributing

Feel free to:
- Add new problems under existing patterns.
- Suggest improvements in code or explanations.
- Submit pull requests with additional patterns.