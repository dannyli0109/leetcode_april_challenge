## Day19

### [Search in Rotated Sorted Array](https://leetcode.com/explore/featured/card/30-day-leetcoding-challenge/530/week-3/3304/)

---

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., `[0,1,2,4,5,6,7]` might become `[4,5,6,7,0,1,2]`).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of O(log n).

**Example 1:**

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

**Example 2:**
```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

- find the piviot for the rotated array first using binary search
- then do the binary search

```cs
public class Solution {
    public int Search(int[] nums, int target) {
        int left = 0;
        int right = nums.Length - 1;
        while(left < right) {
            int mid = (left + right) / 2;
            if (mid == left && nums[left + 1] < nums[left]) left = left + 1;
            else if (nums[left] > nums[mid]) right = mid;   
            else if (nums[right] < nums[mid]) left = mid;
            else break;
        }
        int piviot = left;

        left = 0;
        right = nums.Length - 1;
        while(left <= right) {
            int mid = (left + right) / 2;
            int newMid = (mid + piviot) % nums.Length;
            if (nums[newMid] == target) return newMid;
            if (nums[newMid] > target) right = mid - 1;
            if (nums[newMid] < target) left = mid + 1;
        }
        
        return -1;
    }
}
```