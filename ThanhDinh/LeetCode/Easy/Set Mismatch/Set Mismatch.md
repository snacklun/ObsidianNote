# Description

You have a set of integers `s` which originally contains all numbers from `1` to `n`.

Due to an error:

- One number appears **twice**
    
- One number is **missing**
    

You are given an integer array `nums` representing the corrupted set.

Return the number that occurs twice and the number that is missing, **in the form `[duplicate, missing]`**.

---

## Examples

**Example 1**

Input: `nums = [1,2,2,4]`  
Output: `[2,3]`  
Explanation:  
The number `2` appears twice and the number `3` is missing.

---

**Example 2**

Input: `nums = [1,1]`  
Output: `[1,2]`  
Explanation:  
The number `1` appears twice and the number `2` is missing.

---

## Constraints

- `2 <= nums.length <= 10^4`
    
- `1 <= nums[i] <= 10^4`
    
- `nums` contains exactly one duplicated number and one missing number
    

---

## Problem Type

- Array
    
- Hash Table
    
- Math
    

---

## Goal

Identify:

- the number that appears **twice**
    
- the number that is **missing**
    

and return them as `[duplicate, missing]`.