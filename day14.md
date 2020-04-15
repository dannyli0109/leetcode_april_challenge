## Day14

### [Perform String Shifts](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/529/week-2/3299/)

---

You are given a string `s` containing lowercase English letters, and a matrix `shift`, where `shift[i] = [direction, amount]`:

- `direction` can be `0` (for left shift) or `1` (for right shift). 
- `amount` is the amount by which string `s` is to be shifted.
- A left shift by 1 means remove the first character of `s` and append it to the end.
- Similarly, a right shift by 1 means remove the last character of `s` and add it to the beginning.
Return the final string after all operations.

**Example 1:**

```
Input: s = "abc", shift = [[0,1],[1,2]]
Output: "cab"
Explanation: 
[0,1] means shift to left by 1. "abc" -> "bca"
[1,2] means shift to right by 2. "bca" -> "cab"
```

**Example 2:**

```
Input: s = "abcdefg", shift = [[1,1],[1,1],[0,2],[1,3]]
Output: "efgabcd"
Explanation:  
[1,1] means shift to right by 1. "abcdefg" -> "gabcdef"
[1,1] means shift to right by 1. "gabcdef" -> "fgabcde"
[0,2] means shift to left by 2. "fgabcde" -> "abcdefg"
[1,3] means shift to right by 3. "abcdefg" -> "efgabcd"
```
 
**Constraints:**

- `1 <= s.length <= 100`
- `s` only contains lower case English letters.
- `1 <= shift.length <= 100`
- `shift[i].length == 2`
- `0 <= shift[i][0] <= 1`
- `0 <= shift[i][1] <= 100`

---

- we only care about the staring postion of the string after the shift, therefore, we can -1 when it is a left shift and +1 when it is a right shift
- is `start < 0`, we add the length of the string to wrap the string around
- do modulos to aviod start posion bigger than the length of the string

```cs
public class Solution {
    public string StringShift(string s, int[][] shift) {
        int start = 0;
        foreach (int[] move in shift) {
            int dir = move[0] == 0 ? -1 : 1;
            start = (start + dir * move[1]) % s.Length;
        }
        if (start < 0) start += -(start / s.Length - 1) * s.Length;
        return s.Substring(s.Length - start, start) + s.Substring(0, s.Length - start);
    }
}
```