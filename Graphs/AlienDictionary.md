


```java

 public String alienOrder(String[] words) {
        StringBuilder res = new StringBuilder();
        Map<Character, Integer> inDegree = new HashMap<>();
        Map<Character, Set<Character>> map = new HashMap<>();
        
        initialize(words, inDegree, map);
        
        for (int i = 0; i < words.length - 1; i++) 
            getEdge(words[i], words[i + 1], inDegree, map);
        
        Queue<Character> q = new LinkedList<>();
        
        for (char c : inDegree.keySet()) 
            if (inDegree.get(c) == 0) q.offer(c);
        
        // Kahns algorithm
        while (!q.isEmpty()) {
            char curr = q.poll();
            res.append(curr);
            for (char c : map.get(curr)) {
                inDegree.put(c, inDegree.get(c) - 1);
                if (inDegree.get(c) == 0) q.offer(c);
            }
        }
        
        // Needs to be equal to number of characters which is . the map size, else NO POSSIBLE TOPOLOGICAL SORT
        if (res.length() != map.size()) return "";
        
        return res.toString();    
    }

    
    // This method gets the edge by comparing characters 1 by 1. (If they are equal, go to next character
    public void getEdge(String word1, String word2, Map<Character, Integer> inDegree, Map<Character, Set<Character>> map) {
        
        int i = 0, j = 0;
        
        while (i < word1.length() && j < word2.length()) {
            char c1 = word1.charAt(i++);
            char c2 = word2.charAt(j++);
            if (c1 == c2) continue;
            
            //Dont forget about duplicate edges
            if (map.get(c1).contains(c2)) return;

            inDegree.put(c2, inDegree.get(c2) + 1);
            map.get(c1).add(c2);
            return;
        }
    }
    
    public void initialize(String[] words, Map<Character, Integer> inDegree, Map<Character, Set<Character>> map) {
        for (String word : words) {
            for (char c : word.toCharArray()) {
                inDegree.put(c, 0);
                map.put(c, new HashSet<>());
            }
        }
    }
```