
# Trie (HashMap implementation)

```java
public class Trie {
    
    TrieNode root;
    
    class TrieNode {
        Map<Character, TrieNode> children = new HashMap<>();
        boolean isWord;

        public TrieNode() {
        }
        
    }
    
    /** Initialize your data structure here. */
    public Trie() {
        root = new TrieNode();  
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        
        TrieNode curr = root;
        
        for (int i = 0; i < word.length(); i++) {
            char c = word.charAt(i);
            curr.children.putIfAbsent(c, new TrieNode(c))
            curr = curr.children.get(c); 
        }

        curr.isWord = true;   
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        TrieNode curr = root;
        
        for (char c : word.toCharArray()) {
            
            if (curr.children.containsKey(c)) {
                curr = curr.children.get(c);
            } else {
                return false;
            }    
        }
        
        return curr.isWord;  
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        
        TrieNode curr = root;
        
        for (char c : prefix.toCharArray()) {
            if (curr.children.containsKey(c)) {
                curr = curr.children.get(c);
            } else {
                return false;
            }  
        }
        
        return true;
        
    }
}
```
