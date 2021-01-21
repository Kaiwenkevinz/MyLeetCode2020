相似题目：
- [寻找旋转排序数组中的最小值](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)
### 二分查找 100%
主要在于搞清楚 nums[l], nums[m] 和 nums[r] 之间的关系
```java
class Solution {
    public int findMin(int[] nums) {
        int l = 0;
        int r = nums.length - 1;
        while (l < r) {
            if (nums[l] < nums[r]) { // 二分后得到的区间不存在旋转，最小值就是最左数
                return nums[l];
            }
            int m = l + ((r - l) >> 1);
            if (nums[l] > nums[m]) {    // l...m 之间发生了旋转, m...r之间为严格递增，最小数在m左边，包括m
                r = m;
            } else if (nums[l] < nums[m]) { // l..m 之间为严格递增，而且nums[l] >= nums[r]，说明l...m之间的数都是大于m...r, 最小值在m右边，不包括m
                l = m + 1;
            } else {    // nums[l] == nums[m] , 10111, 11101，无法分辨
                l++;
            }
        }
        return nums[l];
    }
}  
```
