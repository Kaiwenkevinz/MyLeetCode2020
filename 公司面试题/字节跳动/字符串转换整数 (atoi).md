### 模拟
```java
class Solution {
    public int myAtoi(String s) {
        int n = s.length();
        if (n == 0) {
            return 0;
        }

        char[] charArray = s.toCharArray();
        // 移除前导空格
        int index = 0;
        while (index < n) {
            if (charArray[index] == ' ') {
                index++;
            } else {
                break;
            }
        }
        // 判断全是空格的极端情况
        if (index == n) {
            return 0;
        }
        // 如果第一个元素是 + 或 -，则记录sign
        int sign = 1;
        if (charArray[index] == '+') {
            sign = 1;
            index++;
        } else if (charArray[index] == '-') {
            sign = -1;
            index++;
        }
        // 判断极端情况如 ['+'] ['-']
        if (index == n) {
            return 0;
        }
        // 如果第一个元素不是数字，直接返回0
        if (charArray[index] < '0' || charArray[index] > '9') {
            return 0;
        }
        // 到这一步说明可以开始进行数字转换了
        int res = 0;
        while (index < n) {
            char c = charArray[index];
            if (c < '0' || c > '9') {
                break;
            }
            // 判断是否需要截断
            // res == Integer.MAX_VALUE / 10 && c - '0' >= 7 用来判断 2147483648 这种除以10是等于MAX_VALUE，但是其实是大于MAX_VALUE的漏网之鱼
            // res == Integer.MIN_VALUE / 10 && c - '0' >= 8 同上
            if ((res > Integer.MAX_VALUE / 10) || (res == Integer.MAX_VALUE / 10 && c - '0' >= 7)) {     
                return Integer.MAX_VALUE;
            }
            if ((res < Integer.MIN_VALUE / 10) || (res == Integer.MIN_VALUE / 10 && c - '0' >= 8)) {
                return Integer.MIN_VALUE;
            }
            // 字符到数字转换
            res = res * 10 + sign * (c - '0');
            index++;
        }
        return res;
    }
}
```
