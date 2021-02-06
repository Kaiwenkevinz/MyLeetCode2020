```java
class Solution {
    public int calculate(String s) {
        Stack<Integer> stack = new Stack<>();
        int num = 0;
        int sign = '+';
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);

            // c是空格而且c不是最后一个字符
            if (c == ' ' && i != s.length() - 1) {
                continue;
            }

            // c是数字
            if (Character.isDigit(c)) {
                num = num * 10 + (c - '0');
            }

            // c是符号，或者是最后一个字符（数字或空格）
            // 开始结算
            if (!Character.isDigit(c) || i == s.length() - 1) {
                int pre;
                switch(sign) {
                    case '+':
                        stack.push(num);
                        break;
                    case '-':
                        stack.push(-num);
                        break;
                    case '*':
                        pre = stack.pop();
                        stack.push(pre * num);
                        break;
                    case '/':
                        pre = stack.pop();
                        stack.push(pre / num);
                        break;
                    default:
                        break;
                }
                num = 0;
                sign = c;
            }
        }
        
        int res = 0;
        for (int n : stack) {
            res += n;
        }
        return res;
    }
}
```
