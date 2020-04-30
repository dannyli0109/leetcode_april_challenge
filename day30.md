## Day30 

### [Check If a String Is a Valid Sequence from Root to Leaves Path in a Binary Tree](https://leetcode.com/explore/featured/card/30-day-leetcoding-challenge/532/week-5/3315/)

---

Given a binary tree where each path going from the root to any leaf form a **valid sequence**, check if a given string is a **valid sequence** in such binary tree. 

We get the given string from the concatenation of an array of integers `arr` and the concatenation of all values of the nodes along a path results in a **sequence** in the given binary tree.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/12/18/leetcode_testcase_1.png)

```
Input: root = [0,1,0,0,1,0,null,null,1,0,0], arr = [0,1,0,1]
Output: true
Explanation: 
The path 0 -> 1 -> 0 -> 1 is a valid sequence (green color in the figure). 
Other valid sequences are: 
0 -> 1 -> 1 -> 0 
0 -> 0 -> 0
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/12/18/leetcode_testcase_2.png)

```
Input: root = [0,1,0,0,1,0,null,null,1,0,0], arr = [0,0,1]
Output: false 
Explanation: The path 0 -> 0 -> 1 does not exist, therefore it is not even a sequence.
```

**Example 3:**

![](https://assets.leetcode.com/uploads/2019/12/18/leetcode_testcase_3.png)

```
Input: root = [0,1,0,0,1,0,null,null,1,0,0], arr = [0,1,1]
Output: false
Explanation: The path 0 -> 1 -> 1 is a sequence, but it is not a valid sequence.
```

**Constraints:**

- `1 <= arr.length <= 5000`
- `0 <= arr[i] <= 9`
- Each node's value is between [0 - 9].

---

- Check if the current node has the same value as the front of the array, if it does, remove the first element from the array.
- return true if the current node is a end node and the array's length is one and the element in the array is the same as the current node

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
    public bool IsValidSequence(TreeNode root, int[] arr) {
        TreeNode head = root;
        if (head == null) return false;
        if (head.val != arr[0]) return false;
        if (head.val == arr[0] && arr.Length == 1) {
            if (head.left != null || head.right != null) return false;
            return true;
        }
        int[] newArr = new int[arr.Length - 1];
        for (int i = 1; i < arr.Length; i++) {
            newArr[i - 1] = arr[i];
        }
        return IsValidSequence(head.left, newArr) || IsValidSequence(head.right, newArr);  
    }
}
```