## Day3

### [Maximum Subarray](https://leetcode.com/explore/other/card/30-day-leetcoding-challenge/528/week-1/3285/)

---

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

**Example:**

```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

**Follow up:**

If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

--- 

- if accumulate value is less then zero, then, just drop it, otherwise, keep adding


```cs
public class Solution {
    public int MaxSubArray(int[] nums) {
        int ans = nums[0];
        int a = 0;
        for (int i = 0; i < nums.Length; i++){
            a += nums[i];
            if (a > ans) ans = a;
            if (a < 0) a = 0;
        }
        return ans;
    }
}
```

- dp will work as well:

```cs
public class Solution {
    public int MaxSubArray(int[] nums) {
        int[] dp = new int[nums.Length];
        dp[0] = nums[0];
        int result = nums[0];
        for (int i = 1; i < nums.Length; i++){
            dp[i] = (int)Math.Max(dp[i - 1] + nums[i], nums[i]);
            if (dp[i] > result) result = dp[i];
        }
        return result;
    }
}
```