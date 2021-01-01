### 直接遍历, O(n)
```java
import java.util.ArrayList;
public class Solution {
    public int minNumberInRotateArray(int [] array) {
        if(array.length == 0) {
            return 0;
        }
        if(array.length == 1) {
            return array[0];
        }
        
        for(int i = 1; i < array.length; i++) {
            if(array[i] < array[i - 1]) {
                return array[i];
            }
        }
        return 0;
    }
}
```

### 二分法, O(logn)
- ex：[1, 0]  
while的判断条件是`start <= end`, 如果start + 1 == end时， mid永远是0，start一直是0，造成死循环，所以加一个临界点 `start + 1 == end` 就return end。
- ex: [3,0,3,3,3] 和 [3,3,3,0,3]  
此时无法判断应该挪动start还是end指针，所以使用顺序查找

最差情况，O(n)  
平均情况，O(logn)

```java
import java.util.ArrayList;
public class Solution {
    public int minNumberInRotateArray(int [] array) {
        if(array.length == 0) {
            return 0;
        }

        int start = 0;
        int end = array.length - 1;
        int mid = 0;
        while(start <= end) {
            if (start + 1 == end) { // 不 return 无法跳出循环，mid永远为0
                return array[end];
            }
            
            mid = start + (end - start) / 2;
            
            if(array[mid] == array[end] && array[start] == array[end]) {
                // {3,0,3,3,3}, start = mid = end
                return findInOrder(array, start, end);
            }
            
            if(array[mid] <= array[end]) {
                end = mid;
            } else if (array[mid] >= array[end]){
                start = mid;
            }
        }
        return array[mid];
    }
    
    private int findInOrder(int[] array, int start, int end) {
        for (int i = start + 1; i <= end; i++) {
            if(array[i] < array[i - 1]) {
                return array[i];
            }
        }
        return 0;
    }
}
```
