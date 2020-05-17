
# Graphs

## Representations
* Edge List 
* Adjacency List 
* Adjacency Matrix

## Time Complexity of DFS/BFS

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

    for (neighbors : node.getNeighbrs()) 
            dfs(neighbor); 
    
}
```


# Iterative DFS

```java
  
// DFS Nonrecusrive traversal

void DFS(Node node) {

    Stack<> s = new Stack<>();
    Set<> visited = new HashSet<>();
    s.push(node) 

    while (!s.empty()) {
        curr = s.pop() // pop from stack
        if (visited.contains(curr)) continue;
        
        // process vertex
        visited.add(curr) // add to visited set
            
        for (neighbor : getNeighbrs(Node)) 
            s.push(neighbor);         
         
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

*Note: here nodes are represented as ints rather than a node class)*

*Note: Topological Sort only applies to directed graphs)*


## Topological Sort (Reverse PostOrder Method)

```java

public List<Integer> topologicalSort(Graph G) {

    stack = new Stack<Integer>();
    visited = new HashSet<Integer>;
    ArrayList<Integer> res = new ArrayList

    for (int node : G.getNodes()) 
        if (!visited.contains(v)) topologicalSort(node, stack, visited)
    
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

## Topological Sort (Kahns Algorithm)


# Detect Cycle in Graph

## Detect Cycle (Union Find Method)

1. Iterate through edges
2. Union each pair of vertices in each edge
3. If any two vertices in an edge belong same set, we have a cycle

```java
     public boolean hasCycle(int n, int[][] edges) {
        
        // Great Union find example
        int[] parent = new int[n];
        Arrays.fill(parent, -1);
        
        for (int[] edge : edges){
            int a = find(edge[0], parent);
            int b = find(edge[1], parent);
            if (a == b) return true;
            union(a, b, parent);
        }
        
        return false;   
    }
    
    public int find(int i, int[] parent) {
        if (parent[i] <  0) return i;
        parent[i] = find(parent[i], parent);
        return parent[i];  
        
    }
    
    // Optimization = weighted union find
    public void union(int a, int b, int[] parent){
        if (parent[a] < parent[b]) {
            parent[a] += parent[b];
            parent[b] = a;
        } else {
            parent[b] += parent[a];
            parent[a] = b;
        }  
    }
    
```

## Detect Cycle (DFS Undirected Graph)


```java

public void detectCycle(Graph g) {
    Set<Node> visited = new HashSet<>();

    for (Node node : g.getVertices) {
        if (visited.contains(node)) continue;
        if (detectCycleDfs(node, visited, null))
            return true;
    }
}

public boolean detectCycleDfs(Node node, Set<Node> visited, Node parent) {
    if (visited) return true;
    visited.add(node);
    for (Node neighbor : node.getNeighbors) {
        // Only search nodes that aren't parent
        if (neighbor != parent) {
            if (detectCycleDfs(neighbor, visited, node)) 
                return true;
        }
    }
    
    return false;
}
```


# Kruskal's Algorithm

Used to find Minimum Spanning Tree of a graph

Algorithm:

1. Sort Edges by lowest weight
2. Create Disjoint Set and call findSet on each pair of vertices
3. If in different sets, add the edge to the result, else continue

```java
     public List<Edge> kruskals(Graph G) {
       
        List<Edge> edges = G.getEdges();
        edges.sort((a,b) -> a.weight - b.weight)
        List<Edge> res = new ArrayList<>();
     
        // Great Union find example
        int[] parent = new int[G.size()];
        Arrays.fill(parent, -1);
        
        for (int[] edge : edges){
            int a = find(edge[0], parent);
            int b = find(edge[1], parent);
            if (a == b) continue;
            union(a, b, parent);
            res.add(edge)
        }
        
        return res;   
    }
    
    public int find(int i, int[] parent) {
        if (parent[i] <  0) return i;
        parent[i] = find(parent[i], parent);
        return parent[i];  
        
    }
    
    // Optimization = weighted union find
    public void union(int a, int b, int[] parent){
        if (parent[a] < parent[b]) {
            parent[a] += parent[b];
            parent[b] = a;
        } else {
            parent[b] += parent[a];
            parent[a] = b;
        }  
    }
    
```

# Dijkstra's Algorithm


Algorithm:
First create 3 data structures:

distance[v], init all distances to Integer.MAX_VALUE
parent[v]
priorityQueue<Node> (a, b) - > dist[a] - dist[b]

Let distance of source vertex from start = 0
Let distance of al other vertices from start = infinity

	1. Pop the next unvisited vertex from the shortest known distance from start
	2. Add popped vertex to visited, because it's impossible to find a shorter distance (not necessary I think)
	3. For current/popped vertex, calculate distnace of all the neighbors
		a. Neighbor's distance = current vertex distanced + edge weight
		b. If this distance < current disntace in array, update the distance (remove/add from queue, And set current vertex as parent.

> Result if dijkstras gives you shortest path to all nodes
> Recreate any single path using the parent array
 
 
 ```java
       
public void dijkstras(Graph G, int source) {

    Map<Integer, List<Edge>> adj = G.getAdjacencyList();

    int[] dist = new int[G.size()];
    int[] parent = new int[G.size()];

    // Set all nodes distance to inifinity, set source dist to zero
    // Set parents to -1
    Arrays.fill(dist, Integer.MAX_VALUE);
    Arrays.fill(parent, -1);
    dist[source] = 0;

    PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> dist[a]- dist[b])
    pq.add(source);
    
    // Visited Set not necessary!!, just for reference
    Set<Integer> visited = new HashSet<>();

    while (!pq.isEmpty() {

        int curr = pq.poll();

        for (Edge e: adj.get(curr)) {
            int target = e.target;
            int weight - e.weight;
            int dist = dist[curr] + weight;

            if (dist < dist[target]) {
                dist[target] = dist
                //Remove and re-add to pq, cause might be in it
                pq.remove(target);
                pq.add(target);
                parent[target] = curr;
            }
        }
    }  
}

// Need edge class to store both target and weight (still an adjacency list List<Edge>)
class Edge {
    int target;
    int weight;
}

// Build path given target
List<Integer> getPath(int[] parent, int target) {
    List<Integer> path = new ArrayList<>();
    while (parent[target] != -1) {
        path.add(target);
        target = parent[target];
    }
    path.add(target);
    Collections.reverse(path);
    return path;
}
    
```

