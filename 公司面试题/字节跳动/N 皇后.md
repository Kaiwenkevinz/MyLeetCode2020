### 回溯
回溯题目有个特点，就是找到结果的过程可以用树形图来表示，然后可以用树的遍历来穷举所有可能性。
```java
class Solution {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> res = new ArrayList<>();  // 保存结果
        char[][] board = new char[n][n];
        for (int i = 0; i < n; i++) {   // 初始化棋盘
            for (int j = 0; j < n; j++) {
                board[i][j] = '.';
            }
        } 
        solve(board, 0, res);
        return res;
    }

    public void solve(char[][] board, int row, List<List<String>> res) {
        // base case，每一行都走完了，说明找到了结果
        if (row == board.length) {
            List<String> temp = construct(board);
            res.add(temp);
            return;
        }
        for (int col = 0; col < board.length; col++) {
            // 判断能否把棋子下在board[row][col]位置
            if (valid(board, row, col)) {
                // 可以下在row, col位置
                board[row][col] = 'Q';
                // 继续下一行
                solve(board, row + 1, res);
                // 回溯，reset
                board[row][col] = '.';
            }
        }
    }

    public boolean valid(char[][] board, int row, int col) {
        // 判断棋子上方
        for (int i = 0; i < row; i++) {
            if (board[i][col] == 'Q') {
                return false;
            } 
        }
        // 判断棋子的斜线
        for (int i = row, j = col; i >= 0 && j < board.length; i--, j++) {
            if (board[i][j] == 'Q') {
                return false;
            }
        }
        // 另一条斜线
        for (int i = row, j = col; i >= 0 && j >= 0; i--, j--) {
            if (board[i][j] == 'Q') {
                return false;
            }
        }
        return true;
    }

    public List<String> construct(char[][] matrix) {
        List<String> res = new ArrayList<>();
        for (char[] array : matrix) {
            res.add(String.valueOf(array));
        }
        return res;
    }
}
```
