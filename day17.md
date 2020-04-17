## Day17

### [Number of Islands](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/530/week-3/3302/)

---

Given a 2d grid map of `'1'`s (land) and `'0'`s (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

```
Input:
11110
11010
11000
00000

Output: 1
```

Example 2:

```
Input:
11000
11000
00100
00011

Output: 3
```

---
- bfs/dfs problem, dfs will be a little bit more efficient?
- create a stack and push coordinate into it if it is island, and make the item in the original array 0, so we don't check them again
- check the neighbour to see if they are island and push into the stack
- when the stack is empty, we get an island

```cs
public class Solution {
    public int NumIslands(char[][] grid) {
        Stack<int[]> stack = new Stack<int[]>();
        int count = 0;
        int[] dirX = new int[] { 0, 1, 0, -1 };
        int[] dirY = new int[] { -1, 0, 1, 0 };
        for (int i = 0; i < grid.Length; i++) {
            for (int j = 0; j < grid[i].Length; j++) {    
                if (grid[i][j] == '0') continue;
                stack.Push(new int[]{i, j});
                grid[i][j] = '0';
                while (stack.Count > 0) {
                    int[] cord = stack.Pop();
                    for (int k = 0; k < 4; k ++) {
                        int newI = cord[0] + dirY[k];
                        int newJ = cord[1] + dirX[k];
                        if (newI >= 0 && newI < grid.Length && newJ >=0 && newJ < grid[0].Length) {
                            if (grid[newI][newJ] == '1') {
                                stack.Push(new int[]{newI, newJ});
                                grid[newI][newJ] = '0';
                            }
                        }
                    }  
                }
                if (stack.Count == 0) count++;
            }
        }
        return count;
    }
}
```