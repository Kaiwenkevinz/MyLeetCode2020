### BFS
```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
    public int maxDepth(Node root) {
        int res = 0;
        Queue<Node> queue = new LinkedList<>();
        queue.offer(root);
        while (queue.size() > 0 && root != null) {
            int len = queue.size();
            res++;
            for (int i = 0; i < len; i++) {
                Node node = queue.poll();
                for (Node n : node.children) {
                    queue.offer(n);
                }
            }
        }
        return res;
    }
}
```

### 递归
```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
    public int maxDepth(Node root) {
        if (root == null) {
            return 0;
        }
        int depth = 0;
        for (Node node : root.children) {
            depth = Math.max(depth, maxDepth(node));
        }
        return depth + 1;
    }
}
```
