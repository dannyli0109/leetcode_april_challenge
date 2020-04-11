## Day9

### [Backspace String Compare](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/529/week-2/3291/)

---

Given two strings `S` and `T`, return if they are equal when both are typed into empty text editors. `#` means a backspace character.

**Example 1:**

```
Input: S = "ab#c", T = "ad#c"
Output: true
Explanation: Both S and T become "ac".
```

**Example 2:**

```
Input: S = "ab##", T = "c#d#"
Output: true
Explanation: Both S and T become "".
```

**Example 3:**

```
Input: S = "a##c", T = "#a#c"
Output: true
Explanation: Both S and T become "c".
```

**Example 4:**

```
Input: S = "a#c", T = "b"
Output: false
Explanation: S becomes "c" while T becomes "b".
Note:

1 <= S.length <= 200
1 <= T.length <= 200
S and T only contain lowercase letters and '#' characters.
```

**Follow up:**

Can you solve it in `O(N)` time and `O(1)`space?

- build the string and see if they are the same
- **There's another way using pointer and reverse traverse**

```cs
public class Solution {
    public bool BackspaceCompare(string S, string T) {
        char[] ss = new char[S.Length];
        int sLength = 0;
        char[] tt = new char[T.Length];
        int tLength = 0;
        
        foreach (char str in S) {
            if (str == '#') {
                sLength = (int)MathF.Max(0, sLength - 1);
            }
            else {
                ss[sLength] = str;
                sLength ++;
            }
        }
        
        foreach (char str in T) {
            if (str == '#') {
                tLength = (int)MathF.Max(0, tLength - 1);
            }
            else {
                tt[tLength] = str;
                tLength ++;
            }
        }
        if (sLength != tLength) return false;
        for (int i = 0; i < sLength; i++) {
            if (ss[i] != tt[i]) return false;
        }
        
        return true;
    }
}
```