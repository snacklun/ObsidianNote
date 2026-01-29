# Idea

In a correct set:

- Numbers from `1` to `n` should appear **exactly once**
    

Because of the error:

- One number appears **twice**
    
- One number appears **zero times**
    

We just need to **count occurrences** or **compare expected vs actual values**.

---

## Approach 1 — Hash Map / Counter (Recommended)

### Steps

1. Count how many times each number appears.
    
2. Iterate from `1` to `n`:
    
    - Count `2` → duplicated number
        
    - Count `0` → missing number
        

---

### Python Code

```
from collections import Counter
from typing import List

class Solution:
    def findErrorNums(self, nums: List[int]) -> List[int]:
        count = Counter(nums)
        n = len(nums)

        duplicate = None
        missing = None

        for i in range(1, n + 1):
            if count[i] == 2:
                duplicate = i
            elif count[i] == 0:
                missing = i

        return [duplicate, missing]

```

---

## Approach 2 — Math + Set (Recommend)

### Idea

- Expected sum of numbers from `1` to `n` is known.
    
- The difference between the expected sum and the actual sum reveals the missing number.
    
- The difference between `sum(nums)` and `sum(set(nums))` reveals the duplicate.
    

---

### Python Code

```
class Solution:
    def findErrorNums(self, nums: List[int]) -> List[int]:
        n = len(nums)

        expected_sum = n * (n + 1) // 2
        actual_sum = sum(nums)
        unique_sum = sum(set(nums))

        duplicate = actual_sum - unique_sum
        missing = expected_sum - unique_sum

        return [duplicate, missing]
```


---

## Approach 3 — In-Place Marking (O(1) Extra Space)

⚠️ This modifies the input array.

### Idea

- Use each number as an index.
    
- If a number’s index is already negative → duplicate found.
    
- The index left positive at the end → missing number.
    

---

### Python Code

```
class Solution:
    def findErrorNums(self, nums: List[int]) -> List[int]:
        duplicate = -1
        missing = -1

        for x in nums:
            idx = abs(x) - 1
            if nums[idx] < 0:
                duplicate = abs(x)
            else:
                nums[idx] *= -1

        for i in range(len(nums)):
            if nums[i] > 0:
                missing = i + 1

        return [duplicate, missing]

```
---

## Dry Run (Example: `nums = [1,2,2,4]`)

Expected numbers: `1 2 3 4`

|Number|Count|
|---|---|
|1|1|
|2|2 ← duplicate|
|3|0 ← missing|
|4|1|

Result: `[2,3]`

---

## Complexity

|Approach|Time|Space|
|---|---|---|
|Counter|O(n)|O(n)|
|Math + Set|O(n)|O(n)|
|In-place marking|O(n)|O(1)|

---

## Key Takeaways

- Exactly **one duplicate** and **one missing** number exist.
    
- `Counter` is the clearest and safest solution.
    
- In-place marking is optimal but modifies input.
    
- Mathematical reasoning avoids explicit counting.
    

---

## Common Mistakes

- Forgetting to check numbers from `1` to `n`
    
- Returning `[missing, duplicate]` instead of `[duplicate, missing]`
    
- Using a `set` and forgetting it removes duplicates
    

---

## Interview Tip

Say:

> “Since the array should contain numbers from 1 to n exactly once, I detect the duplicated number by counting occurrences and identify the missing number by checking which value never appears.”

That explanation is clear, confident, and interviewer-friendly ✅