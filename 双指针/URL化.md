```java
class Solution {
    public String replaceSpaces(String S, int length) {
        int i = length - 1;  // 指针指向最后一个有效字符
        int j = S.length() - 1;  // 指针指向新字符串的最后一个位置
        char[] array = S.toCharArray();
        while (i >= 0) {
            if (array[i] == ' ') {
                array[j--] = '0';
                array[j--] = '2';
                array[j--] = '%';
            } else {
                array[j--] = array[i]; 
            }
            i--;
        }
        return String.valueOf(array).substring(j + 1, array.length);  // j 之前的字符串都是旧的，舍弃不要
    }
}
```
