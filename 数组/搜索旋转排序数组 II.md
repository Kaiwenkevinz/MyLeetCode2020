### 二分查找 1ms 79.62%
分情况讨论：
- `nums[l] > nums[m]`
- `nums[l] < nums[m]`
- `nums[l] == nums[m]`
```java
class Solution {
    public boolean search(int[] nums, int target) {
        int l = 0;
        int r = nums.length - 1;
        int n = nums.length;
        while (l <= r) {
            int m = l + ((r - l) >> 1);
            if (nums[m] == target) {
                return true;
            } else if (nums[l] == nums[m]) {    // l...m 都是相同元素, 可能是 10111，也可能是 11101
                l++;
            } else if (nums[l] > nums[m]) {     // l...m 发生了旋转, 如 256 0 012
                if (target > nums[m] && target <= nums[n - 1]) {
                    l = m + 1;
                } else {
                    r = m - 1;
                }
            } else {            // l...m 没有旋转，如 123 4 567
                if (target >= nums[l] && target < nums[m]) {
                    r = m - 1;
                } else {
                    l = m + 1;
                }
            }
        }

        return false;
    }
}
```
