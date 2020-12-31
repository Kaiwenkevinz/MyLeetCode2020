```java
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
import java.util.HashMap;

public class Solution {
    private static HashMap<Integer, Integer> memo = new HashMap<>();
    
    public TreeNode reConstructBinaryTree(int [] pre,int [] in) {
        for(int i = 0; i < in.length; i++) {
            memo.put(in[i], i);
        }
        return helper(pre, in, 0, pre.length - 1, 0, in.length - 1);
    }
    
    public static TreeNode helper(int[] pre, int[] in, int preStart, int preEnd, int inStart, int inEnd) {
        if(preStart > preEnd || inStart > inEnd) {
            return null;
        }
    
        TreeNode root = new TreeNode(pre[preStart]);
        int rootIndexIn = memo.get(pre[preStart]);
        int inLeftLen = rootIndexIn - inStart;
        
        root.left = helper(pre, in, preStart + 1, preStart + inLeftLen, inStart, rootIndexIn - 1);
        root.right = helper(pre, in, preStart + inLeftLen + 1, preEnd, rootIndexIn + 1, inEnd);
    
        return root;
    }
}
```
