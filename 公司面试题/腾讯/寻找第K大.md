### Partition， O(klogn)
```java
public class Solution {
     public static int partition(int[] a, int left, int right) {
        int pivot = a[right];    // 设pivot为最右边的数
        int i = left - 1; // i和它左边的元素都小于pivot, 初始设为 left - 1 代表没有元素小于pivot
        int cur = left;    // 以cur为基准遍历
        while(cur <= right - 1) { // 当cur到达pivot的左边一个位置时，跳出遍历
            if(a[cur] < pivot) {  // a[cur] 小于pivot的值
                i++;              // i在++之前，i左边包括i的数都是小于pivot的，所以要交换的位置在i++
                swap(a, cur, i);  // 交换a[cur] 和 a[i]之后，i左边包括i的数依然是小于pivot的
            }
            cur++;    // 继续下一次循环
        }
         // 此时跳出循环，意味着cur = right, cur已经到达pivot位置，而且i包括i左边的数都是小于pivot的

        swap(a, i + 1, right); // a[...i] < pivot, i + 1位置的数是第一个大于pivot的数，所以交换i + 1和pivot的位置right
        return i + 1;    // 返回pivot的位置
    }

    public static void swap(int[] a, int i, int j) {
        int temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }

    public static int findKth(int[] a, int n, int K) {
        int targetIndex = n - K; // 第k大的数换句话说就是第n - K + 1小的数，因为是zero based index， 所以第K小的数在 n - k 的位置
        int left = 0;
        int right = n - 1;
        int index;
        while(true) {
            index = partition(a, left, right);    
            if(index == targetIndex) {
                return a[index];
            }
            if(index > targetIndex) {    // targetIndex应该在index的左边，缩小right指针
                right = index - 1;
            } else {
                left = index + 1;    // targetIndex应该在index的右边，缩小left指针
            }
        }
    }
}
```
