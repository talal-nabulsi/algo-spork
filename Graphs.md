
# Graphs

## Representations
* Edge List 
* Adjacency List 
* Adjacency Matrix


* DFS/BFS Time Complexity = **O(V + |E|)**, 
* For an undirected graph, the runtime is calculated as **O(V + 2|E|)**


# DFS

```java
//Recursive DFS

void dfs(Node v) {

    if (visited.contains(node)) 
        return;
    
    visited.add(node);
    //vist and process vertex

    for (neighbors : node.getNeighbrs()) {
        if (!visited.contains(node)) 
            dfs(neighbor); 
    }
}
```


# Iterative DFS

```java
  
// DFS Nonrecusrive traversal

void DFS(Vertex v) {

    Stack<> s = new Stack<>();
    Set<> visited = new HashSet<>();
    s.push(v) 

    while (!s.empty()) {
        curr = s.pop() // pop from stack
        
        if (!visited.contains(curr)) {
            
            visited.add(curr) // add to visited set
            // process vertex
            for (neighbor : v.getNeighbrs()) {
                if (!visited.contains(v)) 
                    s.push(neighbor);
                
            }
        }
    }
}

// 1. Pop of the stack
// 2. If not viisted then visit and add unvisited neighbors

```

# BFS

```java

public void bfs(Node v) {
    Queue<> q = new ArrayList<>();
    Set<> visited = new HashSet<>();

    visited.add(node);
    q.push(node);

    while (!q.empty()) {
        
        Node u = q.poll();
        //Process Vertex

        for (neighbor : getNeighbors(node)) {
            if (!visited.contains(neighbor)) {
                visited.add(neighbor); 
                q.push(neighbor);
            }
        }
    }
}
```


# Topological Sort

Only applies to directed graphs

```java

// Reverse Postorder method
public List<Integer> topologicalSort(Graph G) {

    stack = new Stack<Integer>();
    visited = new HashSet<Integer>;
    ArrayList<Integer> res = new ArrayList

    for (int v = 0; i < G.V(); v++) {
        if (!visited.contains(v)) topologicalSort(node, stack, visited)}
    }
    
    while (!stack.isEmtpy()) 
      res.add(stack.pop());
}

private topologicalSortUtil(int node, Stack<Integer> stack, HashSet<Integer> visited) {
    visited.add(node)
    
    for (int node : getAllNeighbors(v)) 
        if(!visited.contains(node)) {topologicalSortUtil(node, stack, visited);}
    
    stack.push(v, stack, visited);

}

```


# Kruskal's Algorithm



# Djistrak's Algorithm
