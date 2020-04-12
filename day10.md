## Day10

### [Min Stack](https://leetcode.com/explore/featured/card/30-day-leetcoding-challenge/529/week-2/3292/)

---

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- getMin() -- Retrieve the minimum element in the stack.
 

**Example:**

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

- mataining another stack to store the min values

```cs
public class MinStack {
    Stack<int> elements;
    Stack<int> mins;
    /** initialize your data structure here. */
    public MinStack() {
        elements = new Stack<int>();
        mins = new Stack<int>();
    }
    
    public void Push(int x) {
        elements.Push(x);
        if (mins.Any()) {
            if (mins.Peek() > x) {
                mins.Push(x);
            } else {
                mins.Push(mins.Peek());
            }
        } else {
            mins.Push(x);
        }
    }
    
    public void Pop() {
        if (mins.Any()) mins.Pop();
        if (elements.Any()) elements.Pop();
    }
    
    public int Top() {
        return elements.Peek();
    }
    
    public int GetMin() {
        return mins.Peek();
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.Push(x);
 * obj.Pop();
 * int param_3 = obj.Top();
 * int param_4 = obj.GetMin();
 */
```