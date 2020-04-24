## Day23

### [Bitwise AND of Numbers Range](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/531/week-4/3308/)

Given a range [m, n] where 0 <= m <= n <= 2147483647, return the bitwise AND of all numbers in this range, inclusive.

**Example 1:**
```
Input: [5,7]
Output: 4
```

**Example 2:**
```
Input: [0,1]
Output: 0
```

---

- use the power from 0 to the max power of 2 that less than n
- if the remainer of of the current bit is in the range of the last bit and the next bit, then the current bit is 1
- add all the bit that are 1 together

```cs
public class Solution {
    public int RangeBitwiseAnd(int m, int n) {
        int result = 0;
        int index = 1;
        long pow = (long)MathF.Pow(2, index - 1);

        while(pow <= n) {
            if (
                (m % (pow * 2) > pow - 1) && (m % (pow * 2) < pow * 2) &&
                (n % (pow * 2) > pow - 1) && (n % (pow * 2) < pow * 2) &&
                (n - m) < pow
            ) {
                result += (int)pow;
            }
            index++;
            pow = (long)MathF.Pow(2, index - 1);

        }
        return result;
    }
}
```