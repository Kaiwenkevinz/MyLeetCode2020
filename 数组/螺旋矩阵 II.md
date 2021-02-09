### 妙蛙的模拟法 100%

```java
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] matrix = new int[n][n];
        int num = 1;
        int top = 0;
        int bottom = n - 1;
        int left = 0;
        int right = n - 1;
        while (num <= n * n) {
            // 从左到右
            for (int i = left; i <= right; i++) {
                matrix[top][i] = num++;
            }
            top++; // 缩小上边界

            // 从上到下
            for (int i = top; i <= bottom; i++) {
                matrix[i][right] = num++;
            }
            right--; // 缩小右边界

            // 从右到左
            for (int i = right; i >= left; i--) {
                matrix[bottom][i] = num++;
            }
            bottom--; // 缩小下边界

            // 从下到上
            for (int i = bottom; i >= top; i--) {
                matrix[i][left] = num++;
            }
            left++; // 缩小左边界
        }
        return matrix;
    }
}
```
