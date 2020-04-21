## Day20

### [Construct Binary Search Tree from Preorder Traversal](https://leetcode.com/explore/featured/card/30-day-leetcoding-challenge/530/week-3/3305/)

---

Return the root node of a binary **search** tree that matches the given `preorder` traversal.

(Recall that a binary search tree is a binary tree where for every node, any descendant of `node.left` has a value `< node.val`, and any descendant of `node.right` has a value `> node.val`.  Also recall that a preorder traversal displays the value of the `node` first, then traverses `node.left`, then traverses `node.right`.)

 

```
Example 1:

Input: [8,5,1,7,10,12]
Output: [8,5,10,1,7,null,12]
```
![](https://assets.leetcode.com/uploads/2019/03/06/1266.png)

**Note:**

1. `1 <= preorder.length <= 100`
2. The values of `preorder` are distinct.

---

- recursively look for the left child first to see if it fits the parent, if it is, add left child to the parent
- do the same to the right child
- for left child, we want the max value to be the parnet value
- for the right child, we want the min value to be the parent value
- if we run out of the list, we return null
- if the child doesn't fits the parent, we return null

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
    int index = 0;
    public TreeNode BstFromPreorder(int[] preorder) {
        return recursive(preorder, int.MinValue, int.MaxValue);
    }
    
    public TreeNode recursive(int[] preorder, int min, int max) {
        if (index >= preorder.Length) return null;
        if (preorder[index] < min || preorder[index] > max) return null;
        TreeNode parent = new TreeNode(preorder[index++]);
        parent.left = recursive(preorder, min, parent.val);
        parent.right = recursive(preorder, parent.val, max);
        return parent;
    }
}
```