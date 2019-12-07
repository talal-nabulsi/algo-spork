
# Graphs

## Representations
* Edge List
* Adjacency List
* Adjacency Matrix


* DFS/BFS Time Complexity = **O(V + |E|)**, 
* For an undirected graph, the runtime is calculated as **O(V + 2|E|)**


# DFS

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

# Topological Sort




# Kruskal's Algorithm



# Djistrak's Algorithm
