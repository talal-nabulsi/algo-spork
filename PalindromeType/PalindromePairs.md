
https://leetcode.com/problems/palindrome-pairs/

Not terribly hard, but remember all the helper and utils

> Two solutions: Trie is probably the better one overall. Really tricky kind of question that you probably should have seen before to be able to understand

> Overall not too bad though once you understand it: 

> The Leetcode solution article builds a backwards trie to search each word

> I prefer doing a forwards trie and checking each string backwards


> Key Points
1. As you are inserting in the trie, check if the remaining part of string is a palindrome and add that to the list in the current node: Example when inserting  the wrod **banana**: after you insert b, anana is a palindrome so you would add that words index to the list of node b.

```java
// Trie solution is not that hard, just a lot of thinking initially
// Solution article has a really good explanation
// It works by building a backwards trie an checking for these 3 cases 
// Personally I think I prefer building a forwards trie and checking each word backwards
// Just draw it up, it gets a lot easier with examples

//Case 1: Reverse of word is in trie: CAT and TAC
//Case 2: First word is smaller than second. Once you finish matching check if that last node has any palindrome prefixes remaining:
// Example Matching: TAC and CATLOL, you'll get to teh end of the word and see that LOL is a palindrome and thus we can match these 2 as Pair(biggerWord, word)

//Case 3 (slightlly easier cse): First word is larger than second: you hit a word ending but you arent done building the word. Check if the rest of that word is a palindrome
// Example: You are checking the word ananaboo, and oob is also a word. After you match oob, check if anana is a palindrome and you've got a Pair(smallerWord, word)

class Solution {

    public List<List<Integer>> palindromePairs(String[] words) {

        TrieNode trie = new TrieNode();

        // Build the Trie
        for (int i = 0; i < words.length; i++) {
            String word = words[i];
            TrieNode currTrie = trie;
            for (int j = 0; j < word.length(); j++) {
                if (hasPalindromeRemaining(word, j)) 
                    currTrie.palindromePrefixRemaining.add(i);
                
                char c = word.charAt(j);
                currTrie.next.putIfAbsent(c, new TrieNode());
                currTrie = currTrie.next.get(c);
            }
            currTrie.wordEnding = i;
        }

        // Find pairs
        List<List<Integer>> pairs = new ArrayList<>();
        for (int i = 0; i < words.length; i++) {
            String word = reverse(words[i]);
            TrieNode currTrie = trie;
            
            for (int j = 0; j < word.length(); j++) {
                // Check for pairs of case 3
                if (currTrie.wordEnding != -1 && hasPalindromeRemaining(word, j)) 
                    pairs.add(Arrays.asList(currTrie.wordEnding, i));
                
                // Move down to the next trie level.
                char c = word.charAt(j);
                currTrie = currTrie.next.get(c);
                if (currTrie == null) break;
            }
            
            if (currTrie == null) continue;
            
            // Check for pairs of case 1. Note the check to prevent non distinct pairs. 
            // This means the reverse of the word exists
            if (currTrie.wordEnding != -1 && currTrie.wordEnding != i) 
                pairs.add(Arrays.asList(i, currTrie.wordEnding));
            
            // Check for pairs of case 2
            for (int other : currTrie.palindromePrefixRemaining) 
                pairs.add(Arrays.asList(other, i));
            
        }

        return pairs;
    }
    
    
    // ---------------------Helper Methods------------------------------
    
    
    // Is the given string a palindrome after index i?
    // Tip: Leave this as a method stub in an interview unless you have time
    // or the interviewer tells you to write it. The Trie itself should be
    // the main focus of your time.
    public boolean hasPalindromeRemaining(String s, int i) {
        int p1 = i;
        int p2 = s.length() - 1;
        while (p1 < p2) {
            if (s.charAt(p1) != s.charAt(p2)) return false;
            p1++; p2--;
        }
        return true;
    }
    
    public String reverse(String s) {
        return new StringBuilder(s).reverse().toString();
    }
    
    class TrieNode {
        public int wordEnding = -1; // We'll use -1 to mean there's no word ending here.
        public Map<Character, TrieNode> next = new HashMap<>();
        public List<Integer> palindromePrefixRemaining = new ArrayList<>();
    }

}

```



## The OG Less opitmal solution with hashmap

```java

public List<List<Integer>> palindromePairs(String[] words) {
        
        List<List<Integer>> result = new ArrayList<>();
        Map<String, Integer> map = new HashMap<>();
        for (int i = 0; i < words.length; i++) map.put(words[i], i);
        
        for (int i = 0; i < words.length; i++) {
            String word = words[i];
            
            String reversed = reverse(word);
            if (map.containsKey(reversed) && map.get(reversed) != i) {
                addPair(i, map.get(reversed), result);
            }
            if (isPalindrome(word) && map.get("") != null && map.get("") != i) {
                addPair(i, map.get(""), result);
                addPair(map.get(""), i, result);
            }
            
            for (int j = 0; j < word.length() - 1; j++) {
                
                String part1 = word.substring(0, j + 1);
                String part2 = word.substring(j + 1);
                
                if (isPalindrome(part1)) {
                    String rev = reverse(part2);
                    if (map.containsKey(rev) && map.get(rev) != i) addPair(map.get(rev), i, result);
                }
                
                 if (isPalindrome(part2)) {
                    String rev = reverse(part1);
                    if (map.containsKey(rev) && map.get(rev) != i) addPair(i, map.get(rev), result);
                }
                    
            }
                  
            
        }
        
        return result;
        
    }
```
