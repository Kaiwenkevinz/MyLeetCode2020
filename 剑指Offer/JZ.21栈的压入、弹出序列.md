### 模拟法
```java
import java.util.ArrayList;

public class Solution {
    public boolean IsPopOrder(int [] pushA,int [] popA) {
        int i = 0;
        int j = 0;
        ArrayList<Integer> temp = new ArrayList<>();
        while(i < pushA.length) {
            if(pushA[i] == popA[j]) {
                i++;
                j++;
                while(j < popA.length && temp.get(temp.size() - 1) == popA[j]) {
                    temp.remove(temp.size() - 1);
                    j++;
                }
            } else {
                temp.add(pushA[i]);
                i++;
            }
        }
        
        return temp.size() == 0;
    }
}
```
