## Day22

### [Subarray Sum Equals K](https://leetcode.com/explore/featured/card/30-day-leetcoding-challenge/531/week-4/3307/)

---

Given an array of integers and an integer k, you need to find the total number of continuous subarrays whose sum equals to k.

**Example 1:**
```
Input:nums = [1,1,1], k = 2
Output: 2
```

**Note:**

1. The length of the array is in range [1, 20,000].
2. The range of numbers in the array is [-1000, 1000] and the range of the integer **k** is [-1e7, 1e7].

--- 

- we can reduce dp to a 1 d array given that `dp[i + 1, j]  = dp[i, j] - nums[j]`

```cs
public class Solution {
    public int SubarraySum(int[] nums, int k) {
        int[] dp = new int[nums.Length];
        int count = 0;
        for (int i = 0; i < nums.Length; i++) {
            for (int j = i; j < nums.Length; j++) {
                if (j == 0) {
                    dp[j] = nums[j];
                }
                else if (i == j) {
                    dp[j] -= nums[j - 1];
                }
                else {
                    dp[j] = dp[j - 1] + nums[j];
                }
                if (dp[j] == k) count++;
            }
        }
        return count;
    }
}
```