## 📝 Algorithm Explanation Note Template

**Document Type:** Algorithm Observation/Technical Note

| **Field**               | **Detail / Placeholder**                                 |
| ----------------------- | -------------------------------------------------------- |
| **Algorithm Name**      | Reverse Polish Notation Evaluation (RPN Stack Algorithm) |
| **Category**            | Stack / Expression Evaluation                            |
| **Author/Observer**     | [Your Name]                                              |
| **Date of Observation** | [DD/MM/YYYY]                                             |
| **Source/Reference**    | LeetCode – Evaluate Reverse Polish Notation              |

---

## I. Overview and Purpose

### 1. Goal

Evaluate an arithmetic expression written in Reverse Polish Notation and return the final integer result.

> Reverse Polish Notation places operators after operands, eliminating the need for parentheses and operator precedence rules.

### 2. Constraints / Prerequisites

- Input must be a valid RPN expression
    
- Operators supported: +, -, *, /
    
- Division truncates toward zero
    
- No division by zero
    
- Intermediate values fit in 32-bit integer range
    
- Tokens are processed left to right
    

---

## II. Core Logic and Mechanics

### 3. Key Data Structures

**Stack**

- Stores intermediate numeric values
    
- Ensures last-in-first-out evaluation
    
- Perfect match for postfix expression rules
    

---

### 4. Step-by-Step Procedure

1. **Initialization**
    
    Create an empty stack to hold operands.
    
2. **Iteration**
    
    Traverse tokens from left to right.
    
3. **Operand Handling**
    
    If the token is a number:
    
    - Convert to integer
        
    - Push onto stack
        
4. **Operator Handling**
    
    If the token is an operator:
    
    - Pop right operand
        
    - Pop left operand
        
    - Apply operator
        
    - Push result back to stack
        
5. **Termination**
    
    After processing all tokens:
    
    - The stack contains exactly one value
        
    - That value is the final result
        

---

### 5. Illustration with detailed steps / Example / Code

Example:

tokens = ["2","1","+","3","*"]

Execution trace:

Step 1: push 2 → stack [2]  
Step 2: push 1 → stack [2, 1]  
Step 3: '+' → pop 1 and 2 → push 3 → stack [3]  
Step 4: push 3 → stack [3, 3]  
Step 5: '*' → pop 3 and 3 → push 9 → stack [9]

Final result = 9

---

### C# Implementation

```csharp
public class Solution
{
    public int EvalRPN(string[] tokens)
    {
        Stack<int> stack = new Stack<int>();

        foreach (string token in tokens)
        {
            if (token != "+" && token != "-" && token != "*" && token != "/")
            {
                stack.Push(int.Parse(token));
                continue;
            }

            int rightValue = stack.Pop();
            int leftValue = stack.Pop();

            int result = 0;

            if (token == "+")
                result = leftValue + rightValue;
            else if (token == "-")
                result = leftValue - rightValue;
            else if (token == "*")
                result = leftValue * rightValue;
            else
                result = leftValue / rightValue; // truncates toward zero in C#

            stack.Push(result);
        }

        return stack.Peek();
    }
}
```

---

## III. Performance Analysis

### 6. Time Complexity

O(n)

Each token is processed exactly once. Stack operations (push/pop) are constant time.

### 7. Efficiency Notes

- Stack guarantees constant-time insertion and removal
    
- No recursion or expression tree required
    
- Memory usage grows only with number of operands
    

This makes the algorithm optimal for single-pass evaluation.

---

## IV. Applications and Review

### 8. Use Cases

- Expression evaluation in compilers
    
- Stack-based virtual machines
    
- Calculator interpreters
    
- Postfix expression engines
    
- Bytecode execution models
    

---

### 9. Observer Notes / Review Points

- Operand order matters: left operand is popped second
    
- Integer division behavior must match truncation rule
    
- Stack must never underflow (guaranteed by valid input)
    
- Useful pattern for many parsing problems
    
- Can extend to support more operators easily
    

> Reverse Polish evaluation is a classic example of stack-driven computation and appears frequently in interview questions and language interpreters.