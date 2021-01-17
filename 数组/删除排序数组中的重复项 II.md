相似题目：  
[删除排序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)
### 双指针 O(n) 1ms 81.79%
```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int i = 1;
        int count = 1;
        int removed = 0;
        while (i + removed < nums.length) {
            if (nums[i] != nums[i - 1]) {
                count = 1;
                i++;
            } else if (count < 2) {
                count++;
                i++;
            } else {  // nums[i] == nums[i - 1] and count >= 2
                remove(nums, i);
                removed++;
            } 
        }
        return i;
    }

    public void remove(int[] nums, int pos) {
        for (int i = pos + 1; i < nums.length; i++) {
            nums[i - 1] = nums[i];
        }
    }
}
```
