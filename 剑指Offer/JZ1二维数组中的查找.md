### 暴力解
一个一个找，O(n*m)时间
```java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        if (matrix.length == 0 || matrix[0].length == 0) {
            return false;
        }

        for (int[] row : matrix) {
            for (int n : row) {
                if (n == target) {
                    return true;
                }
            }
        }

        return false;
    }
}
```

### 二分查找
逐行二分查找， O(nlogm)，n行，每行m个元素
```java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        if (matrix.length == 0 || matrix[0].length == 0) {
            return false;
        }

        for (int[] row : matrix) {
            if (binaryFind(row, target)) {
                return true;
            }
        }
        return false;
    }

    // 二分查找
    // return true 找到
    // return false 没找到
    public boolean binaryFind(int[] array, int target) {
        int start = 0;
        int end = array.length - 1;
        int m;
        while (start <= end) {
            m = start + ((end - start) >> 1);
            if (array[m] == target) {
                return true;
            } else if (array[m] > target) {
                end = m - 1;
            } else {
                start = m + 1;
            }
        }
        return false;
    }
}
```

### 利用有序特性
利用行和列都有序的特性，每次删去一行或一列，O(m+n)
```java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        if (matrix.length == 0 || matrix[0].length == 0) {
            return false;
        }

        int n = matrix.length - 1;
        int m = matrix[0].length - 1;
        int row = 0;
        int col = m;
        while (row <= n && col >= 0) {
            if (matrix[row][col] == target) {
                return true;
            } else if (matrix[row][col] > target) {
                col--;
            } else {
                row++;
            }
        }
        return false;
    }
}
```
