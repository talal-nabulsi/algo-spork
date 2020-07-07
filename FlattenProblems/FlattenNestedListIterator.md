// Actually pretty easy problem
// Just put them all on stack in reverse order


```java
public class NestedIterator implements Iterator<Integer> {

    private Stack<NestedInteger> stack;

    public NestedIterator(List<NestedInteger> nestedList) {
        stack = new Stack<>();
        flattenList(nestedList);
    }

    @Override
    public Integer next() {
        return hasNext() ? stack.pop().getInteger() : null;
    }

    @Override
    public boolean hasNext() {
        while (!stack.isEmpty()) {
            if (stack.peek().isInteger()) return true;
            flattenList(stack.pop().getList());
        }
        return false;
    }

    // push all items in nestedList onto stack, in REVERSE order
    private void flattenList(List<NestedInteger> list) {
        for (int i = list.size() - 1; i >= 0; i--) 
            stack.push(list.get(i));
    }
}

// Alternative solution because apparently you shouldn't call
// hasNext in next
class NestedIterator2 implements Iterator<Integer> {
    private Stack<NestedInteger> stack;

    public NestedIterator2(List<NestedInteger> nestedList) {
        stack = new Stack<>();
        enstack(nestedList);
    }
    
    // Same as flattenList above but make sure top is an int
    private void enstack(List<NestedInteger> list) {        
        for (int i = list.size() - 1; i >= 0; i--) 
            stack.push(list.get(i));
        
        
        while (!stack.isEmpty() && !stack.peek().isInteger()) 
            enstack(stack.pop().getList());
        
    }

    @Override
    public Integer next() {
        Integer res = stack.pop().getInteger();
        if (!stack.isEmpty() && !stack.peek().isInteger()) 
            enstack(stack.pop().getList());
        
        return res;
    }

    @Override
    public boolean hasNext() {
        return !stack.isEmpty();
    }
}

```java