# Idea

Reverse Polish Notation processes operators **after** operands.

We use a stack:

- Push numbers onto the stack
    
- When an operator appears:
    
    - Pop the top two numbers
        
    - Apply the operator
        
    - Push the result back
        

At the end, the stack contains the final answer.

---

## Approach — Stack Simulation (Recommended)

### Steps

- Create an empty stack
    
- Loop through each token
    
- If token is a number → push to stack
    
- If token is an operator:
    
    - Pop right operand
        
    - Pop left operand
        
    - Apply operation
        
    - Push result back
        
- Return final stack value
    

Important detail:

Division must truncate toward zero → use `int(a / b)` instead of `//`

---

### Python Code

```
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        stack = []

        for token in tokens:
            if token not in {"+", "-", "*", "/"}:
                stack.append(int(token))
                continue

            right_value = stack.pop()
            left_value = stack.pop()

            if token == "+":
                stack.append(left_value + right_value)
            elif token == "-":
                stack.append(left_value - right_value)
            elif token == "*":
                stack.append(left_value * right_value)
            else:
                stack.append(int(left_value / right_value))

        return stack[-1]

```

---

## Dry Run (Example 1)

tokens = ["2","1","+","3","*"]

|Step|Token|Stack|
|---|---|---|
|1|2|[2]|
|2|1|[2,1]|
|3|+|[3]|
|4|3|[3,3]|
|5|*|[9]|

Final result = 9

---

## Complexity

- **Time Complexity:** O(n)
    
- **Space Complexity:** O(n)
    

Where `n` = number of tokens.

---

## Key Takeaways

- RPN evaluation is a classic stack problem
    
- Operators always use the last two numbers
    
- Order matters: left operand is popped second
    
- Division must truncate toward zero
    

---

## Common Mistakes

- Reversing operand order
    
- Using floor division `//` for negative values
    
- Forgetting to push result back to stack
    

---

## Interview Tip

Say:

> “I simulate Reverse Polish evaluation using a stack. Every operator consumes the last two operands and pushes the computed result back.”