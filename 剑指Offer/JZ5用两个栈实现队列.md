 #### 加上try catch判断特殊情况
 ```java
 import java.util.Stack;

public class Solution {
    Stack<Integer> stack1 = new Stack<Integer>();
    Stack<Integer> stack2 = new Stack<Integer>();
    
    public void push(int node) {
        stack1.push(node);
    }
    
    public int pop() {
        if(!stack2.empty()) {
            return stack2.pop();
        } else {
            while(!stack1.empty()) {
                stack2.push(stack1.pop());
            }
        }
        try{
            return stack2.pop();
        } catch(Exception e) {
            System.out.println("queue is empty");
        }
        
        return -1;
    }
}
 ```
 #### 双stack
 - push O(1)
 - pop O(n)
```java
import java.util.Stack;

public class Solution {
    Stack<Integer> stack1 = new Stack<Integer>();
    Stack<Integer> stack2 = new Stack<Integer>();
    
    public void push(int node) {
        stack1.push(node);
    }
    
    public int pop() {
        int res;
        while(!stack1.empty()) {
            stack2.push(stack1.pop());
        }
        res = stack2.pop();
        while(!stack2.empty()) {
            stack1.push(stack2.pop());
        }
        
        return res;
    }
}
```
