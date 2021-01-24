### 回溯，DFS，集合，无剪枝 9.11% 
```java
class Solution {
    private List<List<Integer>> res;
    private Set<List<Integer>> set;
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        res = new ArrayList<>();
        set = new HashSet<>();
        Arrays.sort(candidates);
        dfs(candidates, 0, target, new ArrayList<Integer>());

        return new ArrayList<>(set);
    }

    private void dfs(int[] candidates, int idx, int target, List<Integer> path) {
        // 在进入这一层之前，检查上一层带下来的参数
        if (target < 0) { // 从根到上一层的path已经超出限制，退出当前path
            return;
        }
        if (target == 0) { // 从根到上一次的path符合我们要找的path，将path加入主数组，并退出当前path
            set.add(new ArrayList<>(temp));
            return;
        }
        
        // 以根为 candidates[i]， 扩展子树
        for (int i = idx; i < candidates.length; i++) {
            path.add(candidates[i]);  // 将父节点加入路径
            dfs(candidates, i + 1, target - candidates[i], path);   // DFS 向下一层，candidates[i]已经使用过了，传入candidates[i + 1] 作为下一层的父节点
            path.remove(path.size() - 1);
        }
    }
}
```

### 回溯+剪枝  99.91% 
```java
class Solution {
    private List<List<Integer>> res;
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        res = new ArrayList<>();
        Arrays.sort(candidates);
        dfs(candidates, 0, target, new ArrayList<Integer>());

        return res;
    }

    private void dfs(int[] candidates, int idx, int target, List<Integer> path) {
        // 在进入这一层之前，检查上一层带下来的参数
        if (target < 0) { // 从根到上一层的path已经超出限制，退出当前path
            return;
        }
        if (target == 0) { // 从根到上一次的path符合我们要找的path，将path加入主数组，并退出当前path
            res.add(new ArrayList<>(path));
            return;
        }
        
        // 遍历candidates，依次以candidates[i]为根建造子树
        for (int i = idx; i < candidates.length; i++) {
            // 大剪枝
            // candidates[i]已经比target大了，说明后面的candidates[i...] 都比target大，都不可能减去target得零。
            // 直接砍掉已candidates[i...]为根的所有子树，所以用break
            if (candidates[i] > target) {
                break;
            }
            // 小剪枝
            // 跳过当前根，继续看candidates[i+1...], 所以用continue
            if (i > idx && candidates[i] == candidates[i - 1]) {
                continue;
            }

            path.add(candidates[i]);  // 更新路径，将当前节点加入路径

            // DFS 向下一层
            // 由于题目要求每个数字只能使用一次，candidates[i]已经使用过了，传入candidates[i + 1] 作为下一层的父节点
            // 更新下一层的target
            dfs(candidates, i + 1, target - candidates[i], path);   

            // DFS 返回当前层，撤回DFS所造成的新路径，使其恢复成DFS之前的路径
            path.remove(path.size() - 1);
        }
    }
}
```

#### 解释语句: if cur > begin and candidates[cur-1] == candidates[cur] 是如何避免重复的。
```
这个避免重复当思想是在是太重要了。
这个方法最重要的作用是，可以让同一层级，不出现相同的元素。即
                  1
                 / \
                2   2  这种情况不会发生 但是却允许了不同层级之间的重复即：
               /     \
              5       5
                例2
                  1
                 /
                2      这种情况确是允许的
               /
              2  
```
为何会有这种神奇的效果呢？
首先 cur-1 == cur 是用于判定当前元素是否和之前元素相同的语句。这个语句就能砍掉例1。
可是问题来了，如果把所有当前与之前一个元素相同的都砍掉，那么例二的情况也会消失。 
因为当第二个2出现的时候，他就和前一个2相同了。
                
那么如何保留例2呢？
那么就用cur > begin 来避免这种情况，你发现例1中的两个2是处在同一个层级上的，
例2的两个2是处在不同层级上的。
在一个`for循环`中，所有被遍历到的数都是属于`一个层级`的。我们要让一个层级中，
必须出现且只出现一个2，那么就放过第一个出现重复的2，但不放过后面出现的2。
第一个出现的2的特点就是 cur == begin. 第二个出现的2 特点是cur > begin.

> 引用  https://leetcode-cn.com/problems/combination-sum-ii/solution/hui-su-suan-fa-jian-zhi-python-dai-ma-java-dai-m-3/

