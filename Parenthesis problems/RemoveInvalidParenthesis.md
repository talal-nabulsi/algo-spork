# Remove Invalid Parenthesis

## BACKTRACKING!

One of those pretty difficult leetcodes where you probably need to see to get a good answer. Two most popular answers from leetcode discussion: DietPepsi and YaVinci


Really interesting solution. Easy to understand but not very common. Uses a trick to check the string backwards.

```java

     public List<String> removeInvalidParentheses(String s) {
        List<String> output = new ArrayList<>();
        removeHelper(s, output, 0, 0, '(', ')');
        return output;
    }

    // Took me a bit to understand but pretty easy once you understand.
    // The inner for loop is basically to avoid dups!!!!
    // Reverse and do the other way to make even more simple!!
    public void removeHelper(String s, List<String> output, int iStart, int jStart, char openParen, char closedParen) {
        int numOpenParen = 0, numClosedParen = 0;
        for (int i = iStart; i < s.length(); i++) {
            if (s.charAt(i) == openParen) numOpenParen++;
            if (s.charAt(i) == closedParen) numClosedParen++;
            
            if (numClosedParen > numOpenParen) { // We have an extra closed paren we need to remove
                for (int j = jStart; j <= i; j++) // Try removing one at each position, skipping duplicates
                    if (s.charAt(j) == closedParen && (j == jStart || s.charAt(j - 1) != closedParen))
                    // Recursion: iStart = i since we now have valid # closed parenthesis thru i. jStart = j prevents duplicates
                        removeHelper(s.substring(0, j) + s.substring(j + 1, s.length()), output, i, j, openParen, closedParen);
                return; // Stop here. The recursive calls handle the rest of the string.
            }
        }
        // No invalid closed parenthesis detected. Now check opposite direction, or reverse back to original direction.
        String reversed = new StringBuilder(s).reverse().toString();
        if (openParen == '(')
            removeHelper(reversed, output, 0, 0, ')','(');
        else
            // Important here, once you're done checking the reverse, then its valid
            // Don't add the string before you check reverse because it might still be invalid!
            output.add(reversed);
    }


```




YaVinci: Backtracking solution with HashSet. You can improve this do avoid having to use a HashSet for duplicates by tracking the last removed. Inferior to DietPepsis

```java

public List<String> removeInvalidParentheses(String s) {
    int rmL = 0, rmR = 0;
    for (int i = 0; i < s.length(); i++) {
        if (s.charAt(i) == '(') {
            rmL++;
        } else if (s.charAt(i) == ')') {
            if (rmL != 0) {
                rmL--;
            } else {
                rmR++;
            }
        }
    }
    Set<String> res = new HashSet<>();
    dfs(s, 0, res, new StringBuilder(), rmL, rmR, 0);
    return new ArrayList<String>(res);
}

public void dfs(String s, int i, Set<String> res, StringBuilder sb, int rmL, int rmR, int open) {
    if (rmL < 0 || rmR < 0 || open < 0) {
        return;
    }
    if (i == s.length()) {
        if (rmL == 0 && rmR == 0 && open == 0) {
            res.add(sb.toString());
        }        
        return;
    }

    char c = s.charAt(i); 
    int len = sb.length();

    if (c == '(') {
        dfs(s, i + 1, res, sb, rmL - 1, rmR, open);		    // not use (
    	dfs(s, i + 1, res, sb.append(c), rmL, rmR, open + 1);       // use (

    } else if (c == ')') {
        dfs(s, i + 1, res, sb, rmL, rmR - 1, open);	            // not use  )
    	dfs(s, i + 1, res, sb.append(c), rmL, rmR, open - 1);  	    // use )

    } else {
        dfs(s, i + 1, res, sb.append(c), rmL, rmR, open);	
    }

    sb.setLength(len);        
}







```