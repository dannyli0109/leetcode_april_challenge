## Day15

### [Product of Array Except Self](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/530/week-3/3300/)

---

Given an array `nums` of n integers where n > 1,  return an array `output` such that `output[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

**Example:**

```
Input:  [1,2,3,4]
Output: [24,12,8,6]
```

**Constraint:** It's guaranteed that the product of the elements of any prefix or suffix of the array (including the whole array) fits in a 32 bit integer.

**Note:** Please solve it **without division** and in O(n).

**Follow up:**
Could you solve it with constant space complexity? (The output array **does not** count as extra space for the purpose of space complexity analysis.)

---

- for index i, the output will be the product of `0 ... i-1` * `i + 1 ... length -1`
- so we can keeptrack of two lists, one calculate the product up to `i` and the other one calculate the product after `i`
- for `[1,2,3,4]` the product before `i` will be `[1,1,2,6]` and we can do the reverse of num `[4,3,2,1]` to get the sum of the reverse array up to `i` `[1,4,12,24]` if we reverse this list back `[24,12,4,1]` the output at i will be 
```
[1, 1, 2, 6] *
[24,12,4, 1] = 
[24,12,8, 6]
```
```cs
public class Solution {
    public int[] ProductExceptSelf(int[] nums) {
        // [1,2,3,4] => [4,3,2,1]
        // [1,1,2,6] => [1,4,12,24] => 
        // [24,12,4,1]
        int n = nums.Length;
        int[] prefixSums = new int[n];
        int[] suffixSums = new int[n];
        prefixSums[0] = 1;
        suffixSums[0] = 1;
        for (int i = 1; i < n; i++) {
            prefixSums[i] = prefixSums[i - 1] * nums[i - 1];
            suffixSums[i] = suffixSums[i - 1] * nums[n - i];
        }
        int[] outputs = new int[n];
        for (int i = 0; i < n; i++) {
            outputs[i] = prefixSums[i] * suffixSums[n - 1 - i];
        }
        return outputs;
    }
}
```