## Day11

### [Diameter of Binary Tree](https://leetcode.com/explore/featured/card/30-day-leetcoding-challenge/529/week-2/3293/)

---

Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

**Example:**

Given a binary tree

```
          1
         / \
        2   3
       / \     
      4   5   
```

Return **3**, which is the length of the path [4,2,1,3] or [5,2,1,3].

**Note:** The length of path between two nodes is represented by the number of edges between them.

---

- traverse every nodes to get the depth of the left and right sub trees


```cs
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public int CountChildren(TreeNode node, int count) {
        if (node == null) return count;
        else {
            return (int)MathF.Max(CountChildren(node.left, count + 1), CountChildren(node.right, count+1));
        }
    }
    public int DiameterOfBinaryTree(TreeNode root) {
        if (root == null) return 0;
        int result = 0;
        
        Stack<TreeNode> nodes = new Stack<TreeNode>();
        nodes.Push(root);
        while(nodes.Count > 0) {
            TreeNode node = nodes.Pop();
            result = (int)MathF.Max(CountChildren(node.left, 0) + CountChildren(node.right, 0), result);
            if (node.left != null) {
                nodes.Push(node.left);
            }
            if (node.right != null) {
                nodes.Push(node.right);
            }
        }
        return result;
    }
}
```