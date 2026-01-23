# Description

Given two binary strings `a` and `b`, return their sum as a binary string.

The binary string result should not contain leading zeros.

---

## Examples

**Example 1**

Input: a = "11", b = "1"  
Output: "100"  
Explanation:  
11 (binary) + 1 (binary) = 100 (binary).

---

**Example 2**

Input: a = "1010", b = "1011"  
Output: "10101"  
Explanation:  
1010 (binary) + 1011 (binary) = 10101 (binary).

---

## Constraints

- 1 <= a.length, b.length <= 10^4  
- `a` and `b` consist only of '0' or '1' characters.  
- Each string does not contain leading zeros except for the zero itself.

---

## Problem Type

- String
- Math
- Simulation

---

## Goal

Add two binary numbers represented as strings **without using built-in base conversion** functions like `int(a, 2)` or `bin()`.
