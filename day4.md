## Day4

### [Move Zeroes](https://leetcode.com/explore/other/card/30-day-leetcoding-challenge/528/week-1/3286/)

---

Given an array `nums`, write a function to move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Example:**

```
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```

**Note:**

1. You must do this **in-place** without making a copy of the array.
2. Minimize the total number of operations.

- Bubble sort
```cs
public class Solution {
    public void MoveZeroes(int[] nums) {
        for (int i = 0; i < nums.Length; i++) {
            bool swap = false;
            for (int j = 0 ; j < nums.Length - i - 1; j++) {
                if (nums[j] == 0) {
                    int temp = nums[j];
                    nums[j] = nums[j + 1];
                    nums[j + 1] = temp;
                    swap = true;
                }
            }
            if (!swap) break;
        }
    }
}
```

- Two Pointers
  - If the value is not zero keep moving the pointer, and at the end, add zero from the pointer to the end of the array
  - `[0,1,0,3,12]` -> `[1,3,12,3,12]`
    - pointer is 3, from 3 to the end of the array add zeros
    - `[1,3,12,0,0]`

```cs
public class Solution {
    public void MoveZeroes(int[] nums) {
        int n = nums.Length;
        int next = 0;
        foreach(int num in nums) {
            if (num != 0) {
                nums[next] = num;
                next++;
            }   
        }
        
        for (int i = next; i < n; i++) {
            nums[i] = 0;
        }
    }
}
```