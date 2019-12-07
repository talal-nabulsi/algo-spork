# algorithmCheatSheet
Cheat Sheets for algorithms


Complete Binary Tree - All levels except for possibly last are filled and nodes are far left as possible.

Perfect Binary Tree = All levels completely filled

Max nodes at each level i = 2^i. (staring at level 0)

Max nodes in total 2^n−1


# In perfect binary trees there's a cool mathematical relationship between the number of nodes and the height of the tree.

First, there's a pattern to how many nodes are on each level:

Level 0: 2^0=12 
0
 =1 nodes,
Level 1: 2^1=22 
1
 =2 nodes,
Level 22: 2^2=42 
2
 =4 nodes,
Level 33: 2^3=82 
3
 =8 nodes,
etc


```java
public class Solution {
    public int longestPalindromeSubseq(String s) {
        int[][] dp = new int[s.length()][s.length()];
        
        for (int i = s.length() - 1; i >= 0; i--) {
            dp[i][i] = 1;
            for (int j = i+1; j < s.length(); j++) {
                if (s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = dp[i+1][j-1] + 2;
                } else {
                    dp[i][j] = Math.max(dp[i+1][j], dp[i][j-1]);
                }
            }
        }
        return dp[0][s.length()-1];
    }
}


```
