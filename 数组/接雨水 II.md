### CV大法
参考答案 https://leetcode-cn.com/problems/trapping-rain-water-ii/solution/you-xian-dui-lie-de-si-lu-jie-jue-jie-yu-shui-ii-b/  

记不记得住看缘分。。。
```java
import java.util.PriorityQueue;
class Solution {
    public int trapRainWater(int[][] heightMap) {
        int n = heightMap.length;
        int m = heightMap[0].length;
        int ans = 0;
        // 初始化一个最小堆，储存三元组 (x, y, h)，h最小的在堆顶
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> {
            return a[2] - b[2];
        });
        // 初始化二维数组用来记录处理过的板子
        boolean[][] visited = new boolean [n][m];
        // 将四周最外围放入最小堆，从最外圈开始往里收
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (i == 0 || i == n - 1 || j == 0 || j == m - 1) {
                    pq.offer(new int[] {i, j, heightMap[i][j]});
                }
            }
        }
        // 对于堆顶的元素：
        //      取出堆顶元素，此时元素为最外围的高度最低的板子
        //      以这块板子为中心，上下左右探测是否能注水
        int[] dirs = {-1, 0, 1, 0, -1};
        while (pq.size() != 0) {
            int[] top = pq.poll();
            visited[top[0]][top[1]] = true;
            for (int k = 0; k < 4; k++) {
                int nx = top[0] + dirs[k];
                int ny = top[1] + dirs[k + 1];
                // 判断位置是否有效
                if (nx >= 0 && nx < n && ny >= 0 && ny < m && !visited[nx][ny]) {
                    if (heightMap[nx][ny] < top[2]) {
                        ans += top[2] - heightMap[nx][ny];
                        pq.offer(new int[] {nx, ny, top[2]});
                    } else {
                        pq.offer(new int[] {nx, ny, heightMap[nx][ny]});
                    }
                    visited[nx][ny] = true;
                }
            }
        }

        return ans;
    }
}
```
