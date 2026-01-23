# Idea

- Iterate over each possible starting index in `haystack`.
- For each position, check if `needle` matches character by character.
- Return the index if a match is found.
- Return -1 if no match is found.

---

## C# Code

```csharp
public static int StrStr(string haystack, string needle)
{
    if (needle.Length == 0)
        return 0;

    int hLen = haystack.Length;
    int nLen = needle.Length;

    for (int i = 0; i <= hLen - nLen; i++)
    {
        int j;
        for (j = 0; j < nLen; j++)
        {
            if (haystack[i + j] != needle[j])
                break;
        }

        if (j == nLen)
            return i;
    }

    return -1;
}
Complexity
Time: O(n * m), where n = length of haystack, m = length of needle.

Space: O(1)
```