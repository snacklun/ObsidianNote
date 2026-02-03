Great idea 👍 — this is a perfect problem to practice **manual binary addition logic**.
# Idea

We simulate how humans add binary numbers:

- Start from the **rightmost digits** (least significant bits).
- Add corresponding digits from `a` and `b`, along with a `carry`.
- The result bit is `(sum % 2)`.
- The new carry is `(sum // 2)`.
- Continue until all digits and carry are processed.
- Reverse the result at the end.

---

## Approach 1 — Two Pointers + Carry (Recommended)

### Steps

- Set pointers `i` and `j` at the end of `a` and `b`.
- Initialize `carry = 0`.
- Loop while `i >= 0` or `j >= 0` or `carry > 0`.
- Convert characters `'0'` / `'1'` to integers manually.
- Append result bits.
- Reverse at the end.

---

### Python Code

```python
def addBinary(a: str, b: str) -> str:
    i = len(a) - 1
    j = len(b) - 1
    carry = 0
    result = []

    while i >= 0 or j >= 0 or carry:
        bit_a = int(a[i]) if i >= 0 else 0
        bit_b = int(b[j]) if j >= 0 else 0

        total = bit_a + bit_b + carry
        result.append(str(total % 2))
        carry = total // 2

        i -= 1
        j -= 1

    return "".join(reversed(result))
````

---

## Approach 2 — Pad Strings to Equal Length

### Idea

- Pad the shorter string with leading zeros.
    
- Add from right to left using a carry.
    
- Build the result.
    

---

### Python Code

```python
def addBinary(a: str, b: str) -> str:
    max_len = max(len(a), len(b))
    a = a.zfill(max_len)
    b = b.zfill(max_len)

    carry = 0
    result = []

    for i in range(max_len - 1, -1, -1):
        total = (a[i] == '1') + (b[i] == '1') + carry
        result.append(str(total % 2))
        carry = total // 2

    if carry:
        result.append('1')

    return "".join(reversed(result))
```

---

## Approach 3 — Recursive Binary Addition (Conceptual)

### Idea

- Add last characters and carry.
    
- Recurse on remaining prefix.
    
- Combine result bits.
    

---

### Python Code

```python
def addBinary(a: str, b: str, carry=0) -> str:
    if not a and not b and not carry:
        return ""

    bit_a = int(a[-1]) if a else 0
    bit_b = int(b[-1]) if b else 0

    total = bit_a + bit_b + carry
    result_bit = str(total % 2)
    new_carry = total // 2

    return addBinary(a[:-1], b[:-1], new_carry) + result_bit
```

---

## Dry Run (Example: a = "1010", b = "1011")

|Step|bit_a|bit_b|carry|total|result bit|
|---|---|---|---|---|---|
|1|0|1|0|1|1|
|2|1|1|0|2|0|
|3|0|0|1|1|1|
|4|1|1|0|2|0|
|end|-|-|1|-|1|

Result: `10101`

---

## Complexity

All approaches:

- **Time Complexity:** `O(n)`
    
- **Space Complexity:** `O(n)` (for result storage)
    

Where `n = max(len(a), len(b))`.

---

## Key Takeaways

- Binary addition works exactly like decimal addition, just base 2.
    
- Always process from right to left.
    
- Keep track of a `carry`.
    
- Avoid converting the whole string to an integer.
    

---

## Common Mistakes

- Forgetting to append the final carry.
    
- Iterating from left to right.
    
- Not handling different string lengths.
    

---

## Interview Tip

Say:

> “I simulate binary addition digit by digit using a carry, starting from the least significant bit, and build the result in reverse.”

That explanation scores points. 💯
