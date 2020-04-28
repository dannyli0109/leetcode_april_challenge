## Day27

### [Maximal Square](https://leetcode.com/explore/other/card/30-day-leetcoding-challenge/531/week-4/3312/)

---

Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

**Example:**

```
Input: 

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

Output: 4
```

--- 

- for each point, check the row i + w and column j + w, if all of them are 1, we increment the w by 1 and continue
- then check the width against the max width, at the end return max * max as the area

```cs
public class Solution {
    public int MaximalSquare(char[][] matrix) {
        int max = 0;
        for (int i = 0; i < matrix.Length; i++) {
            for (int j = 0; j < matrix[i].Length; j++) {
                if (matrix[i][j] == '0') continue;
                int width = 1;
                while(true) {
                    int newI = i + width;
                    int newJ = j + width;
                    if (newI > matrix.Length - 1) break;
                    if (newJ > matrix[i].Length - 1) break;
                    bool valid = true;
                    for (int k = i; k <= newI; k++) 
                        if (matrix[k][newJ] == '0') valid = false;                  
                    for (int k = j; k <= newJ; k++) 
                        if (matrix[newI][k] == '0') valid = false;      
                    if (valid) width++;
                    else break;
                }
                if (max < width) max = width;
            }
        }
        return max * max;
    }
}
```