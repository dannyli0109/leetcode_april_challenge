## Day16

### [Valid Parenthesis String](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/530/week-3/3301/)

---

Given a string containing only three types of characters: '(', ')' and '*', write a function to check whether this string is valid. We define the validity of a string by these rules:

1. Any left parenthesis `'('` must have a corresponding right parenthesis `')'`.
2. Any right parenthesis `')'` must have a corresponding left parenthesis `'('`.
3. Left parenthesis `'('` must go before the corresponding right parenthesis `')'`.
4. `'*'` could be treated as a single right parenthesis `')'` or a single left parenthesis `'('` or an empty string.
5. An empty string is also valid.

**Example 1:
```
Input: "()"
Output: True
```

**Example 2:**
```
Input: "(*)"
Output: True
```

**Example 3:**
```
Input: "(*))"
Output: True
```

**Note:**
- The string size will be in the range [1, 100].

---

- Count the amout of right parenthesis we need at a and store them as variable. 
- We store lower to represent * always act as a ) or empty at that point
- upper to represent * always act as a  (
- if (upper < 0) means there's a leading ), we just return false
- at the end, we only care about if lower is zero
- because the case that right parenthesis more than left parenthesis is already handled by upper < 0
- an important thing to realise is that * has not impact on the ( come after

example:
```
"(*))"
[1,1], [0, 2], [0, 1], [0, 0]
=> lower is zero => return true

"(**()((*"
[1, 1], [0, 2], [0, 3], [1, 4], [0, 3], [1, 4],[2, 5], [1, 6]
=> lower is 1 => return false
```

```cs
public class Solution {
    public bool CheckValidString(string s) {
        int lower = 0;
        int upper = 0;
        for (int i = 0; i < s.Length; i++) {
            if (s[i] == '(') {
                lower++;
                upper++;
            }
            if (s[i] == ')') {
                lower--;
                upper--;
            }
            if (s[i] == '*') {
                lower--;
                upper++;
            }
            if (upper < 0) return false;
            if (lower < 0) lower = 0;
        }
        return lower == 0;
    }
}
```