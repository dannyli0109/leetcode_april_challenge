## Day12

### [Last Stone Weight](https://leetcode.com/explore/other/card/30-day-leetcoding-challenge/529/week-2/3297/)

---

We have a collection of stones, each stone has a positive integer weight.

Each turn, we choose the two heaviest stones and smash them together.  Suppose the stones have weights x and y with x <= y.  The result of this smash is:

If `x == y`, both stones are totally destroyed;
If `x != y`, the stone of weight `x` is totally destroyed, and the stone of weight `y` has new weight `y-x`.
At the end, there is at most 1 stone left.  Return the weight of this stone (or 0 if there are no stones left.)

**Example 1:**

```
Input: [2,7,4,1,8,1]
Output: 1
Explanation: 
We combine 7 and 8 to get 1 so the array converts to [2,4,1,1,1] then,
we combine 2 and 4 to get 2 so the array converts to [2,1,1,1] then,
we combine 2 and 1 to get 1 so the array converts to [1,1,1] then,
we combine 1 and 1 to get 0 so the array converts to [1] then that's the value of last stone.
```

**Note:**

1. `1 <= stones.length <= 30`
2. `1 <= stones[i] <= 1000`

- sort the list everytime to get the biggest two elements until the list is empty or with one element left

```cs
public class Solution {
    public int LastStoneWeight(int[] stones) {
        List<int> stoneList = ((int[])stones).ToList();
        while(stoneList.Count > 1) {
            stoneList.Sort();
            int n = stoneList.Count;
            int n1 = stoneList[n - 1];
            int n2 = stoneList[n - 2];
            int diff = n1 - n2;
            stoneList.RemoveAt(n - 1);
            stoneList.RemoveAt(n - 2);
            if (diff != 0) {
                stoneList.Add(diff);
            }
        }
        if (stoneList.Count == 0) return 0;
        return stoneList[0];
    }
}
```

