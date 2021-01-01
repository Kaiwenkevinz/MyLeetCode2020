### 找数学规律
n 代表台阶树， f(n) 代表跳n级台阶的跳法数  
n = 1, f(1) = 1 = 2^0   
n = 2, f(2) = 2 = 2^1  
n = 3, f(3) = 4 = 2^2  
n = 4, f(4) = 8 = 2^3  

```java
import java.lang.Math;

public class Solution {
    public int JumpFloorII(int target) {
        return (int)Math.pow(2, target - 1);
    }
}
```
