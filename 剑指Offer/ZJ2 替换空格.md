#### 主要考察StringBuffer的用法
- str.charAt()
- str.setCharAt()
- str.insert()

```java
public class Solution {
    public String replaceSpace(StringBuffer str) {
        if(str == null) {
            return "";
        }
        
    	int i = str.length() - 1;
        while(i >= 0) {
            if(str.charAt(i) == ' ') {
                str.setCharAt(i, '%');
                str.insert(i + 1, "20");
            }
            i--;
        }

        return str.toString();
    }
}
```
