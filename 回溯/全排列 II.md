### 回溯
- 剪枝的前提是排序！

```java
class Solution {
    List<List<Integer>> ans;
    public List<List<Integer>> permuteUnique(int[] nums) {
        ans = new ArrayList<>();

        // 排序,为了后面剪枝
        Arrays.sort(nums);
        
        dfs(nums, new ArrayList<Integer>(), new boolean[nums.length]);
        return ans;
    }

    public void dfs(int[] nums, List<Integer> path, boolean[] used) {
        if (path.size() == nums.length) {
            ans.add(new ArrayList<>(path));
            return;
        }

        for (int i = 0; i < nums.length; i++) {
            // 小剪枝
            // i > 0 确保nums[i - 1]有效
            // nums[i] == nums[i - 1] 检查是否遇到了重复值
            // !used[i - 1] 确保 nums[i] 和 nums[i - 1] 是两个不同的分支，而不是在同一个分支中
            if (i > 0 && nums[i] == nums[i - 1] && !used[i - 1]) {
                continue;
            }
            if (!used[i]) {
                used[i] = true;
                path.add(nums[i]);
                dfs(nums, path, used);

                // undo
                used[i] = false;
                path.remove(path.size() - 1);
            }
        }
    } 
}
```
