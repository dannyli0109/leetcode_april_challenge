## Day21

### [Leftmost Column with at Least a One](https://leetcode.com/explore/featured/card/30-day-leetcoding-challenge/530/week-3/3306/)

---

(This problem is an **interactive problem**.)

A binary matrix means that all elements are `0` or `1`. For each **individual** row of the matrix, this row is sorted in non-decreasing order.

Given a row-sorted binary matrix binaryMatrix, return leftmost column index(0-indexed) with at least a `1` in it. If such index doesn't exist, return `-1`.

**You can't access the Binary Matrix directly.**  You may only access the matrix using a `BinaryMatrix` interface:

- `BinaryMatrix.get(x, y)` returns the element of the matrix at index `(x, y)` (0-indexed).
- `BinaryMatrix.dimensions()` returns a list of 2 elements `[n, m]`, which means the matrix is `n * m`.

Submissions making more than `1000` calls to `BinaryMatrix.get` will be judged Wrong Answer.  Also, any solutions that attempt to circumvent the judge will result in disqualification.

For custom testing purposes you're given the binary matrix `mat` as input in the following four examples. You will not have access the binary matrix directly.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/10/25/untitled-diagram-5.jpg)

```
Input: mat = [[0,0],[1,1]]
Output: 0
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/10/25/untitled-diagram-4.jpg)

```
Input: mat = [[0,0],[0,1]]
Output: 1
```

**Example 3:**

![](https://assets.leetcode.com/uploads/2019/10/25/untitled-diagram-3.jpg)

```
Input: mat = [[0,0],[0,0]]
Output: -1
```

**Example 4:**

![](https://assets.leetcode.com/uploads/2019/10/25/untitled-diagram-6.jpg)

```
Input: mat = [[0,0,0,1],[0,0,1,1],[0,1,1,1]]
Output: 1
```
 
**Constraints:**

- `1 <= mat.length, mat[i].length <= 100`
- `mat[i][j]` is either `0` or `1`.
- `mat[i]` is sorted in a non-decreasing way.

---

- for each row, we use binary search to find the left most 1
- find the minimum index of the left most 1

```cs
/**
 * // This is BinaryMatrix's API interface.
 * // You should not implement it, or speculate about its implementation
 * class BinaryMatrix {
 *     public int Get(int x, int y) {}
 *     public IList<int> Dimensions() {}
 * }
 */

class Solution {
    public int LeftMostColumnWithOne(BinaryMatrix binaryMatrix) {
        IList<int> dim = binaryMatrix.Dimensions();
        int rows = dim[0];
        int cols = dim[1];
        int index = 0;
        int result = int.MaxValue;
        for (int i = 0; i < rows; i++){
            int left = 0;
            int right = cols - 1;
            while(left <= right) {
                int mid = (left + right) / 2;
                int num = binaryMatrix.Get(i, mid);
                if (num == 1) {
                    result = (int)MathF.Min(result, mid);
                    right = mid - 1;
                }
                else {
                    left = mid + 1;
                }  
            }
            
        }
        if (result == int.MaxValue) return -1;
        return result;
    }
}
```