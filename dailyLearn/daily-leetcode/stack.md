# Stack

1. [Min Stack](https://leetcode.com/problems/min-stack/)

```java
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

```java
class MinStack {
    Stack<Integer> stack = new Stack<>();
    int min = Integer.MAX_VALUE;
    /** initialize your data structure here. */
    public MinStack() {
    }
    
    public void push(int x) {
        if (x <= min) {
            stack.push(min);//永远有一个小备胎
            min = x;
        }
        stack.push(x);
    }
    
    public void pop() {
        if (min == stack.pop()) {
            min = stack.pop();
        }
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int getMin() {
        return min;
    }
}
```