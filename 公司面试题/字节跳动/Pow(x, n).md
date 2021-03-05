```java
class Solution {
    // x^n = x^(n/2) * x^(n/2)  if n is even
    // x^n = x^(n/2) * x^(n/2) * x   if n is odd
    public double myPow(double x, int n) {
        int abs_n = Math.abs(n);
        if (n >= 0) {
            return helper(x, n);
        } else {
            return 1.0 / helper(x, -n);
        }
    }

    public double helper(double x, int n) {
        if (n == 0) {
            return 1;
        }
        double res = helper(x, n/2);
        if ((n & 1) == 0) {
            return res * res;
        } else {
            return res * res * x;
        }
    }
}
```
