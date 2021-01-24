### 二分 O(nlogn)
先二分法找到最接近x的数，然后在x附近用双指针找到剩余的k - 1个数，最后将结果排序。  
O(nlogn) 时间

```java
import java.util.List;
import java.util.ArrayList;
import java.util.Collections;
class Solution {
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        int l = 0;
        int r = arr.length - 1;
        List<Integer> res = new ArrayList<>();
        while (l < r) {
            int m = l + ((r - l) >> 1);
            if (arr[m] > x) {
                r = m - 1;
            } else if (arr[m] < x) {
                l = m + 1;
            } else {
                l = m;
                break;
            }
        }


        int i = 1;
        int a;
        int b;
        // 1,3  l=1
        if (l > 0 && Math.abs(x - arr[l - 1] <= Math.abs(arr[l] - x)) {
            res.add(arr[l - 1]);
            a = l - 2;
            b = l;
        } else {
            res.add(arr[l]);
            a = l - 1;
            b = l + 1;
        }
        

        while (i < k) {
            if (a < 0 && b < arr.length - 1) {
                res.add(arr[b]);
                b++;
            } else if (a >= 0 && b >= arr.length) {
                res.add(arr[a]);
                a--;
            } else if (Math.abs(x - arr[a]) <= Math.abs(x - arr[b])) {
                res.add(arr[a]);
                a--;
            } else {
                res.add(arr[b]);
                b++;
            }
            i++;
        }
        
        Collections.sort(res);
        return res;
    }
}
```

### 排序 O(nlogn)
按照 arr 中元素与 x 的差值的绝对值排序
```java
import java.util.List;
import java.util.ArrayList;
import java.util.Collections;
import java.lang.Math;
class Solution {
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        List<Integer> res = new ArrayList<>();
        for (Integer n : arr) {
            res.add(n);
        }
        Collections.sort(res, (a,b) -> a == b ? a - b : Math.abs(a-x) - Math.abs(b-x));
        res = res.subList(0, k);
        Collections.sort(res);
        
        return res;
    }
}
```

### 妙妙屋解法- 双指针对撞 O(n)
```java
import java.util.List;
import java.util.ArrayList;
import java.lang.Math;
class Solution {
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        List<Integer> res = new ArrayList<>();
        int l = 0;
        int r = arr.length - 1;
        int count = arr.length - k;
        for (int i = 0; i < count; i++) {
            if (Math.abs(arr[l] - x) <= Math.abs(arr[r] - x)) {
                r--;
            } else {
                l++;
            }
        } 
        for (int j = l; j <= r; j++) {
            res.add(arr[j]);
        }
        return res;
    }
}
```

### 妙妙屋解法
https://leetcode-cn.com/problems/find-k-closest-elements/solution/pai-chu-fa-shuang-zhi-zhen-er-fen-fa-python-dai-ma/  
O(logn + k)
```java
import java.util.List;
import java.util.ArrayList;
class Solution {
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        List<Integer> res = new ArrayList<>();
        int l = 0;
        int r = arr.length - k;
        while (l < r) {
            int mid = l + ((r - l) >> 1);
            if (x - arr[mid] > arr[mid + k] - x) { // 右区间距离x更近，删去左区间
                l = mid + 1;
            } else {
                r = mid;
            }
        }

        for (int i = l; i < l+k; i++) {
            res.add(arr[i]);
        }
        return res;
    }
}
```
