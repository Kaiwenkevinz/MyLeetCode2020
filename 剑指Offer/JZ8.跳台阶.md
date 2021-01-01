### 斐波那契变种

```java
public class Solution {
    public int JumpFloor(int target) {
        // Fibo
        if(target <= 1){
            return 1;
        }
        
        int a = 1;
        int b = 1;
        for(int i = 2; i<= target; i++) {
            int c = a + b;
            a = b;
            b = c;
        }
        
        return b;
    }
}
```
