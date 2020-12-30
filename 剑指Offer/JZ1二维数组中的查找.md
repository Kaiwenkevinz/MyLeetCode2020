### 逐行二分查找， O(nlogm)，n行，每行m个元素
```java
public class Solution {
    public boolean Find(int target, int [][] array) {
        for(int[] row : array) {
            if(findValue(row, target)) {
                return true;
           }
        }
        return false;
    }
    
    public boolean findValue(int[] array, int t) {
        int s = 0;
        int e = array.length - 1;
        while(s <= e) {
            int m = s + (e - s) / 2;
            if(array[m] == t) {
                return true;
            } else if (array[m] > t) {
                e = m - 1;
            } else {
                s = m + 1;
            }
        }
        return false;
    }
}
```

### 利用行和列都有序的特性，O(m+n), n行，每行m个元素
```java
public class Solution {
    public boolean Find(int target, int [][] array) {
        if (array.length == 0) {
            return false;
        }
        
        int row = 0;
        int col = array[0].length - 1;

        while(row < array.length && col >= 0) {
            int n = array[row][col];
            if(target == n) {
                return true;
            } else if(target < n) {
                col--;
            } else {
                row++;
            }
        }
        return false;
    }
}
```
