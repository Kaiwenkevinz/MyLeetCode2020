### ???

```java
import java.util.Arrays;
import java.lang.Math;
class Solution {
    public int[][] dp;
    public int getMoneyAmount(int n) {
        dp = new int[n + 1][n + 1];
        for (int[] row : dp) {
            Arrays.fill(row, Integer.MAX_VALUE);
        }
        return solve(1, n);
    }

    public int solve(int l, int r) {
        // base case
        // 1,1这个区间，只有一个选择，而且也是正确答案，花费0元
        if (l >= r) {
            return 0;
        }
        if (dp[l][r] != Integer.MAX_VALUE) {
            return dp[l][r];
        }

        for (int i = l; i <= r; i++) {
            dp[l][r] = Math.min(dp[l][r], Math.max(i + solve(l, i - 1), i + solve(i + 1, r)));
        }

        return dp[l][r];
    }
}
```
