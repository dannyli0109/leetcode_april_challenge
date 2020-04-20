## Day18

### [Minimum Path Sum](https://leetcode.com/explore/featured/card/30-day-leetcoding-challenge/530/week-3/3303/)

---

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

**Note:** You can only move either down or right at any point in time.

**Example:**

```
Input:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
Output: 7
Explanation: Because the path 1→3→1→1→1 minimizes the sum.
```

---

- bfs, keep track of the distance, if a neighbour have been vistied before check if the current distance to the neighbour is smaller than other paths if it is, update the distance
- as it only move down or right, we only need to check these two directions

```cs
public class Solution {
    public int MinPathSum(int[][] grid) {
        if (grid.Length == 0) return 0;
        int rows = grid.Length;
        int cols = grid[0].Length;
        int[] dirX = new int[]{0, 1};
        int[] dirY = new int[]{1, 0};
        int[,] distance = new int[rows,cols];
        Queue<int[]> queue = new Queue<int[]>();
    
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                distance[i,j] = -1;
            }
        }
        queue.Enqueue(new int[]{0, 0});
        distance[0,0] = grid[0][0];
        while(queue.Any()) {
            int n = queue.Count;
            for (int i = 0; i < n; i++) {
                int[] coord = queue.Dequeue();
                int currentX = coord[1];
                int currentY = coord[0];
                int current = distance[currentY,currentX];
                for (int j = 0; j < 2; j++) {
                    int neighbourX = currentX + dirX[j];
                    int neighbourY = currentY + dirY[j];
                    if (
                        neighbourX >= 0 && neighbourY >= 0 && 
                        neighbourX < cols && neighbourY < rows
                    ) {
                        int neighbour = grid[neighbourY][neighbourX];
                        if (distance[neighbourY,neighbourX] == -1) {
                            queue.Enqueue(new int[] {neighbourY, neighbourX});
                            distance[neighbourY,neighbourX] = neighbour + current;
                        }
                        else {
                            distance[neighbourY,neighbourX] = (int)MathF.Min(distance[neighbourY,neighbourX], current + neighbour);
                        }
                    }
                }
            }
        }
        return distance[rows - 1,cols - 1];
    }
}
```