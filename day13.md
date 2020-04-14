## Day13

### [Contiguous Array](https://leetcode.com/explore/featured/card/30-day-leetcoding-challenge/529/week-2/3298/)

---

Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.

**Example 1:**
```
Input: [0,1]
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.
```

**Example 2:**
```
Input: [0,1,0]
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
```

**Note:** The length of the given binary array will not exceed 50,000.

---

- keep track of the count and the starting and ending index of that count, if two counts meets, the sum will be the end index minus the starting index

```cs
public class Solution {
    public int FindMaxLength(int[] nums) {
        int result = 0;
        int count = 0;
        var map = new Dictionary<int, int[]>();
        map.Add(0, new int[]{-1, 0});
        for (int i = 0; i < nums.Length; i++) {
            count += (nums[i] == 0 ? -1 : 1);
            if (map.ContainsKey(count)) {
                map[count][1] = i;
                result = (int)Math.Max(result, map[count][1] - map[count][0]);
            }
            else {
                map.Add(count, new int[]{i, i});
            }
        }
        return result;
    }
}
```
