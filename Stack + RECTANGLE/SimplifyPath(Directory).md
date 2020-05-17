
# Simplify Path (directories)

> Pretty easy just pop from the stack when you encounter ".."

> This simulates going back a directory


```java

public String simplifyPath(String path) {
    Deque<String> stack = new LinkedList<>();
    Set<String> skip = new HashSet<>(Arrays.asList("..",".",""));
    for (String dir : path.split("/")) {
        if (dir.equals("..") && !stack.isEmpty()) stack.pop();
        else if (!skip.contains(dir)) stack.push(dir);
    }
    String res = "";
    for (String dir : stack) res = "/" + dir + res;
    return res.isEmpty() ? "/" : res;
}

```