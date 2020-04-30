## Day29 (Need revise)

### [Binary Tree Maximum Path Sum](https://leetcode.com/explore/challenge/card/30-day-leetcoding-challenge/532/week-5/3314/)

---

Given **a non-empty** binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain **at least one node** and does not need to go through the root.

**Example 1:**
```
Input: [1,2,3]

       1
      / \
     2   3

Output: 6
```


**Example 2:**

```
Input: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

Output: 42
```

---

- try compute the best of the current sub tree
- when we finish all nodes, look at if the best answer is one of the sub tree

```cs
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    int best = int.MinValue;
    public int MaxPathNode(TreeNode root) {
        if (root == null) return 0;
        int left = (int)MathF.Max(0, MaxPathNode(root.left));
        int right = (int)MathF.Max(0, MaxPathNode(root.right));
        int bestLR = (int)MathF.Max(left, right);
        int bestCombined = (int)MathF.Max(bestLR, left + right);
        best = (int)Math.Max(best, root.val + bestCombined);
        return root.val + (int)MathF.Max(left, right);
    }
    
    public int MaxPathSum(TreeNode root) {
        MaxPathNode(root);
        return best;
    }
}
```