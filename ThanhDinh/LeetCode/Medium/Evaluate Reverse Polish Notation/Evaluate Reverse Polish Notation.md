# Description

You are given an array of strings `tokens` representing an arithmetic expression in **Reverse Polish Notation (RPN)**.

Evaluate the expression and return the final integer result.

Rules:

- Valid operators are `+`, `-`, `*`, `/`
    
- Each operand is either an integer or another expression
    
- Division truncates toward zero
    
- No division by zero will occur
    
- The expression is guaranteed to be valid
    
- All intermediate values fit in 32-bit integer range
    

---

## Examples

**Example 1**

Input: tokens = ["2","1","+","3","*"]  
Output: 9  
Explanation:  
((2 + 1) * 3) = 9

---

**Example 2**

Input: tokens = ["4","13","5","/","+"]  
Output: 6  
Explanation:  
4 + (13 / 5) = 6

---

**Example 3**

Input: tokens = ["10","6","9","3","+","-11","_","/","_","17","+","5","+"]  
Output: 22  
Explanation:  
((10 * (6 / ((9 + 3) * -11))) + 17) + 5 = 22

---

## Constraints

- 1 ≤ tokens.length ≤ 10⁴
    
- tokens[i] is either an operator or an integer in [-200, 200]
    

---

## Problem Type

- Stack
    
- Simulation
    
- Math