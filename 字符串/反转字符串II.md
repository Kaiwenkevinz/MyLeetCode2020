### 模拟法
```java
class Solution {
    public String reverseStr(String s, int k) {
        char[] chars = s.toCharArray();
        int i = 0;
        while (i < chars.length) {
            if (chars.length - i < k) {
                reverse(chars, i, chars.length - 1);
            } else {
                reverse(chars, i, i + k - 1);
            }
            i += 2 * k;
        }
        return new String(chars);
    }

    public void reverse(char[] chars, int l, int r) {
        while (l < r) {
            char temp = chars[l];
            chars[l] = chars[r];
            chars[r] = temp;
            l++;
            r--;
        }
    }
}
```
