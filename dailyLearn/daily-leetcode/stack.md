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

2. [739. Daily Temperatures](https://leetcode.com/problems/daily-temperatures/)

Given a list of daily temperatures T, return a list such that, for each day in the input, tells you how many days you would have to wait until a warmer temperature. If there is no future day for which this is possible, put 0 instead.

For example, given the list of temperatures T = [73, 74, 75, 71, 69, 72, 76, 73], your output should be [1, 1, 4, 2, 1, 1, 0, 0].

```java
class Solution {
    public int[] dailyTemperatures(int[] T) {
        Stack<Integer> stack = new Stack<>();
        int[] ans = new int[T.length];
        for (int i = T.length - 1; i >= 0; i--) {
            while (!stack.isEmpty() && T[i] >= T[stack.peek()]) {
                System.out.println(stack.peek());
                stack.pop();
            }
            ans[i] = stack.isEmpty() ? 0 : stack.peek() - i;
            stack.push(i);
        }
        return ans;
    }
}
```