### 哈希表 + 优先队列
```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        int[] res = new int[k];
        Map<Integer, Integer> map = new HashMap<>();
        Queue<int[]> heap = new PriorityQueue<>((int[] a, int[] b) -> {
            return b[1] - a[1];
        });
        // 哈希表记录元素出现频率
        for (int n :nums) {
            map.put(n, map.getOrDefault(n, 0) + 1);
        }
        // 遍历哈希表，以出现频率为比较，放入最大堆
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            heap.offer(new int[] {entry.getKey(), entry.getValue()});
        }
        // 出堆k次，依次放入返回数组
        for (int i = 0; i < k; i++) {
            res[i] = heap.poll()[0];
        }
        return res;
    }
}
```
