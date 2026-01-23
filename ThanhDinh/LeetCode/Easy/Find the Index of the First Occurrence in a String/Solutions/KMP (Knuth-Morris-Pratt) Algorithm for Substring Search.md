## Idea

The KMP algorithm improves on brute force by avoiding redundant comparisons.

It preprocesses the `needle` to build an **LPS (Longest Prefix Suffix)** array, which tells us where to continue matching after a mismatch.

---

## Steps

1. Build the LPS array for the `needle`:
    - `lps[i]` stores the length of the longest proper prefix of `needle[0..i]` that is also a suffix.
2. Use two pointers:
    - `i` to scan the `haystack`.
    - `j` to scan the `needle`.
3. Compare characters:
    - If `haystack[i] == needle[j]`, increment both `i` and `j`.
    - If `j` reaches `needle.Length`, a match is found.
4. On mismatch:
    - If `j > 0`, set `j = lps[j - 1]` (use LPS to avoid re-checking).
    - Else, move `i` forward.

---

## C# Implementation

```csharp
using System;

public class Solution
{
    // Build LPS array
    private static int[] BuildLPS(string needle)
    {
        int n = needle.Length;
        int[] lps = new int[n];
        int len = 0; // length of previous longest prefix suffix
        int i = 1;

        while (i < n)
        {
            if (needle[i] == needle[len])
            {
                len++;
                lps[i] = len;
                i++;
            }
            else
            {
                if (len != 0)
                {
                    len = lps[len - 1];
                }
                else
                {
                    lps[i] = 0;
                    i++;
                }
            }
        }

        return lps;
    }

    public static int StrStr(string haystack, string needle)
    {
        if (needle.Length == 0)
            return 0;

        int[] lps = BuildLPS(needle);
        int i = 0; // index for haystack
        int j = 0; // index for needle

        while (i < haystack.Length)
        {
            if (haystack[i] == needle[j])
            {
                i++;
                j++;

                if (j == needle.Length)
                    return i - j; // match found
            }
            else
            {
                if (j != 0)
                    j = lps[j - 1];
                else
                    i++;
            }
        }

        return -1; // no match found
    }
}

```