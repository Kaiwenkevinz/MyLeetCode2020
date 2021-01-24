### 回溯 + 剪枝 100%

```java
class Solution {
    public List<List<Integer>> res;
    public List<List<Integer>> combinationSum3(int k, int n) {
        res = new ArrayList<>();
        dfs(k, 1, n, new ArrayList<Integer>());
        return res;
    }

    private void dfs(int k, int val, int target, List<Integer> path) {
        if (target == 0 && k == 0) {
            res.add(new ArrayList<>(path));
            return;
        }
        for (int curN = val; curN <= 9; curN++) {
            // 大剪枝
            if (curN > target || k < 0) { 
                break;
            }
            path.add(curN);
            dfs(k - 1, curN + 1, target - curN, path);
            path.remove(path.size() - 1);
        }

    }
}
```
