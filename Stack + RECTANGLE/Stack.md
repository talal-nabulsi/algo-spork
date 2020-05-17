# Max Rectangle in Histogram

>  Not too hard of a problem, just some tricky details that will be hard to reengineer

> Key point: Every pop from the stack will result in an "Area Calculation Event"

> The stack here represents a queue of the bars that need to be calculated at some future point.

> Because if we have a decreasing height, we can't build any rectancles with the previous heights, so we should calculate all we can

> Use version with stack.push(-1) optimization below! This is Tushar's method without optimization


```java

 public int largestRectangleArea(int[] heights) {
      
        Stack<Integer> stack = new Stack<>();

        // Remember to initialize i here
        int max = 0, area = 0, i = 0;
        
        for (i = 0; i < heights.length;) {
            if (stack.isEmpty() || heights[i] >= heights[stack.peek()]) {
                stack.push(i);
                i++;
            } else {
                int top = stack.pop();
                if (stack.isEmpty())  area = heights[top] * i;
                else  area = heights[top] * (i - stack.peek() - 1);
                
                max = Math.max(area, max);        
            }
        }
           
        // Now i == heights.length, (1 more than the last index)
        while (!stack.isEmpty()) {
            int top = stack.pop();
                
            if (stack.isEmpty()) area = heights[top] * i;
            else area  = heights[top] * (i - stack.peek() - 1);
                
            max = Math.max(area, max);               
        }    
        return max;    
    }

```

> Another small optimzation!!! We can just push -1 onto stack so we don't have to keep checking stack.isEmtpy() and have an if else!

```java

 public int largestRectangleArea(int[] heights) {
        
        Stack<Integer> stack = new Stack<>();
        int max = 0, area = 0, i = 0;
        
        // Optimization so we don't have to check stack.isEmpty() all the time!!
        stack.push(-1);
        
        // Make sure i is initlized outside this loop, or itinitzlie it again after 
        for (i = 0; i < heights.length;) {
            if (stack.peek() == -1 || heights[i] >= heights[stack.peek()]) {
                stack.push(i++);
            } else {
                int top = stack.pop();
                area = heights[top] * (i - stack.peek() - 1);
                max = Math.max(area, max);        
            }
        }
           
        // Now i == heights.length, (1 more than the last index)
        while (stack.peek() != -1 ) {
            int top = stack.pop();
            area  = heights[top] * (i - stack.peek() - 1);
            max = Math.max(area, max);               
        }  
        
        return max;    
    }

```