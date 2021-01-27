### 回溯 + 剪枝 一遍过 100.00%
```java
class Solution {
    List<List<Integer>> ans;
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        ans = new ArrayList<>();
        // 剪枝的前提是排序
        Arrays.sort(nums);
        dfs(nums, 0, new ArrayList<Integer>());
        return ans;
    }

    public void dfs(int[] nums, int begin, ArrayList<Integer> path) {
        ans.add(new ArrayList<>(path));
        for (int i = begin; i < nums.length; i++) {
            if (i > begin && nums[i] == nums[i - 1]) {
                continue;
            }
            path.add(nums[i]);
            dfs(nums, i + 1, path);
            path.remove(path.size() - 1);
        }
    }
}
```
