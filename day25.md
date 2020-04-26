## Day25

### [Jump Game](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/531/week-4/3310/)

---

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

**Example 1**

```
Input: [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

**Example 2:**

```
Input: [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.
```

---

- for each position, if the current position can't reach the upper limit of the pervious positions, we return false, because the current position is unreachable
- otherwise, we update the upper limit to the furthest point we can reach at the current position 

```cs
public class Solution {
    public bool CanJump(int[] nums) {
        int upper = 0;
        for (int i = 0; i < nums.Length; i++) {
            if (i <= upper) {
                int newNum = nums[i];
                upper = (int)MathF.Max(upper, newNum + i);
                if (upper >= nums.Length - 1) return true;
            }
            else {
                return false;
            }
        }
        return upper >= nums.Length - 1;
    }
}
```