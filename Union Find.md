

# Union Find

Things to know
1. Path Compression
2. Ackerman function

# Leetcode 305 : Number of Islands II

Classic Union Find example.


```java

    public List<Integer> numIslands2(int m, int n, int[][] positions) {
        // Can't use matrix because you need a way to number each cell!!!
        int[] parent = new int[m * n];
        List<Integer> res = new ArrayList<>();
        
        Arrays.fill(parent, -1);
        
        int[] dx = {0,1,0,-1};
        int[] dy = {1,0,-1,0};
        
        int count = 0;
        
        for (int[] pos : positions) {
            
            // Initialize land cell and set parent to itself
            int id = pos(pos[0],pos[1], n);
            parent[id] = id;
            // Increment islands
            count++;
            
            for (int i = 0; i < dx.length; i++) {
                int newX = pos[0] + dx[i];
                int newY = pos[1] + dy[i];
                
                int id2 = pos(newX, newY, n);
                
                if (newX >= 0 && newY >= 0 && newX < m && newY < n && parent[id2] != -1) {
                    
                    int x = find(id, parent);
                    int y = find(id2, parent);
                    
                    // If they're not already same island, merge them! (And decrement Island count);
                    if (x != y) {
                        union(x, y, parent);
                        count--;
                    }
                }
            }
            res.add(count);
        }  
        return res;         
    }
    
    public int pos(int i, int j, int n) {
        return i * n + j;
    }
    
    public int find(int i, int[] parent) {
        if (parent[i] == i) return i;
        parent[i] = find(parent[i], parent);
        return parent[i];
    }
    
    public void union(int x, int y, int[] parent) {
        parent[y] = x;
    }

```
