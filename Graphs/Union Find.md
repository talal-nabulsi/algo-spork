

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

ALTERNATIVE SOLUTION - USE PARENT[ID] = -SIZE INSTEAD OF PARENT[ID] = ID
BETTER OVERALL SO YOU CAN TRACK THE "RANK" OF A UNION FIND BASED ON THE SIZE STORED IN PARENT ARRAY AS A NEGATIVE NUMBER
```java

class Solution {
    /**
     * Number of Islands II - A dynamic island formation problem solved with Union Find
     * 
     * Algorithm Category: Union Find (Disjoint Set) with path compression and union by size
     * 
     * Time Complexity: 
     * - O(k * α(m*n)) where k is the number of operations, and α is the inverse Ackermann function
     * - α(m*n) is nearly constant in practice, so effectively O(k)
     * 
     * Space Complexity: O(m*n) for the parent array (combines parent and size information)
     * 
     * Approach:
     * 1. Start with all cells as water (INT_MIN in parent array)
     * 2. For each position, convert to land and make it its own set with size 1 (-1 in parent array)
     * 3. Check all 4 adjacent cells and merge islands when needed
     * 4. Use union by size and path compression for efficiency
     * 5. For roots: parent[i] < 0 and |parent[i]| = size of the set
     * 6. For non-roots: parent[i] = index of its parent
     */
    public List<Integer> numIslands2(int m, int n, int[][] positions) {
        // Parent array that also stores size information for roots
        // parent[i] < 0 -> i is a root and |parent[i]| is the size of the set
        // parent[i] ≥ 0 -> parent[i] is the parent of i
        int[] parent = new int[m * n];
        List<Integer> result = new ArrayList<>();
        
        // Initialize all cells as water (using Integer.MIN_VALUE to distinguish from valid sets)
        Arrays.fill(parent, Integer.MIN_VALUE);
        
        // Direction arrays for checking adjacent cells
        int[] dx = {0, 1, 0, -1};
        int[] dy = {1, 0, -1, 0};
        
        int count = 0;  // Track the current number of islands
        
        for (int[] pos : positions) {
            // Convert position to unique ID
            int id = pos(pos[0], pos[1], n);
            
            // Skip if this position was already turned into land
            if (parent[id] != Integer.MIN_VALUE) {
                result.add(count);
                continue;
            }
            
            // Initialize land cell as its own root with size 1
            parent[id] = -1;  // Negative value indicates it's a root with size 1
            count++;
            
            // Check all 4 adjacent cells
            for (int i = 0; i < dx.length; i++) {
                int newX = pos[0] + dx[i];
                int newY = pos[1] + dy[i];
                int adjId = pos(newX, newY, n);
                
                // Check if adjacent cell is valid and is land
                if (newX >= 0 && newY >= 0 && newX < m && newY < n && parent[adjId] != Integer.MIN_VALUE) {
                    // Find the roots of current cell and adjacent cell
                    int root1 = find(id, parent);
                    int root2 = find(adjId, parent);
                    
                    // If they're from different islands, merge them
                    if (root1 != root2) {
                        union(root1, root2, parent);
                        count--;
                    }
                }
            }
            
            result.add(count);
        }
        
        return result;
    }
    
    /**
     * Converts 2D coordinates to a 1D array index
     */
    public int pos(int i, int j, int n) {
        return i * n + j;
    }
    
    /**
     * Find operation with path compression
     * Returns the root of the set containing i
     */
    public int find(int i, int[] parent) {
        // If i is a root (parent[i] < 0), return i
        if (parent[i] < 0) return i;
        
        // Path compression: point directly to the root
        return parent[i] = find(parent[i], parent);
    }
    
    /**
     * Union operation using size to keep the tree balanced
     * Merges the sets containing x and y (both x and y are roots)
     */
    public void union(int x, int y, int[] parent) {
        // Union by size: attach smaller tree to root of larger tree
        // Remember that for roots, parent[root] = -size
        int sizeX = -parent[x];  // Size of tree rooted at x
        int sizeY = -parent[y];  // Size of tree rooted at y
        
        if (sizeX >= sizeY) {
            // x has larger or equal size, make it the parent
            parent[x] = -(sizeX + sizeY);  // Update size of x's tree
            parent[y] = x;  // Make y point to x
        } else {
            // y has larger size, make it the parent
            parent[y] = -(sizeX + sizeY);  // Update size of y's tree
            parent[x] = y;  // Make x point to y
        }
    }
    
    /**
     * Main method with test cases
     */
    public static void main(String[] args) {
        Solution sol = new Solution();
        
        // Test Case 1: Basic example
        // Each position adds a new isolated island
        int[][] positions1 = {{0,0}, {0,1}, {1,2}, {2,1}};
        System.out.println("Test Case 1: " + sol.numIslands2(3, 3, positions1));
        // Expected: [1, 2, 3, 4]
        
        // Test Case 2: Islands merge example
        // Forms a square pattern that eventually becomes one island
        int[][] positions2 = {{0,0}, {0,1}, {1,1}, {1,0}};
        System.out.println("Test Case 2: " + sol.numIslands2(3, 3, positions2));
        // Expected: [1, 2, 2, 1]
    }
}

```
