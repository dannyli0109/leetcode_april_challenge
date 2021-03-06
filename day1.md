## Day1

### [Single Number](https://leetcode.com/explore/other/card/30-day-leetcoding-challenge/528/week-1/3283/)

---

Given a **non-empty** array of integers, every element appears twice except for one. Find that single one.

**Note:**

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

**Example 1:**

```
Input: [2,2,1]
Output: 1
```

**Example 2:**

```
Input: [4,1,2,1,2]
Output: 4
```

--- 

- Uses bitwise XOR
- This works because if two numbers are the same num ^ num = 0, so all the duplicates will cancel out

```cs
public class Solution {
    public int SingleNumber(int[] nums) {
        int result = 0;
        foreach (int num in nums) {
            result ^= num;
        }
        return result;
    }
}
```