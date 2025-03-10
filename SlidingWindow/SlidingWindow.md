https://leetcode.com/problems/find-all-anagrams-in-a-string/discuss/92007/sliding-window-algorithm-template-to-solve-all-the-leetcode-substring-search-problem



Sliding Window Median - TreeSets

```

/**
 * Sliding Window Median - Data Structure Problem
 * 
 * This algorithm finds the median of all sliding windows of size k in an input array.
 * 
 * Algorithm Type: Balanced TreeSets (used to simulate min and max heaps)
 * Time Complexity: O(n log k) where n is the length of the array and k is the window size
 *   - Each add/remove operation on TreeSet is O(log k)
 *   - We perform these operations for each element
 * Space Complexity: O(k) for storing indices in the two TreeSets
 * 
 * Key Approach:
 * - Use two TreeSets to maintain the window elements by their indices
 * - 'lo' TreeSet contains the smaller half of elements (access largest using last())
 * - 'hi' TreeSet contains the larger half of elements (access smallest using first())
 * - Balance these sets so their sizes differ by at most 1
 * - Calculate median based on the last element of 'lo' and first element of 'hi'
 */
class Solution {
    public double[] medianSlidingWindow(int[] nums, int k) {
        // Result array to store medians for each window
        double[] result = new double[nums.length - k + 1];
        // Tracks the start index of current sliding window
        int start = 0;
          
        // TreeSet to store indices of the smaller half elements
        // Both TreeSets use the same comparator that sorts by value first, then by index
        TreeSet<Integer> lo = new TreeSet<>((a, b) -> (nums[a] != nums[b] ? 
                                           Integer.compare(nums[a], nums[b]) : a - b));
        
        // TreeSet to store indices of the larger half elements
        TreeSet<Integer> hi = new TreeSet<>((a, b) -> (nums[a] != nums[b] ? 
                                           Integer.compare(nums[a], nums[b]) : a - b));
        
        for (int i = 0; i < nums.length; i++) {
            // First add index to the smaller half
            lo.add(i);

            // Move the largest element from smaller half to larger half
            // Using pollLast() to get the largest element from lo
            hi.add(lo.pollLast());
            
            // Rebalance if larger half becomes bigger than smaller half
            // Using pollFirst() to get the smallest element from hi
            if(hi.size() > lo.size()) lo.add(hi.pollFirst());

            // When we have k elements in the window, calculate median and slide the window
            if (lo.size() + hi.size() == k) {
                // Calculate median - if equal sizes, average the middle two elements
                // Otherwise take the max of smaller half
                result[start] = lo.size() == hi.size() ? 
                               nums[lo.last()]/2.0 + nums[hi.first()]/2.0 : 
                               nums[lo.last()]/1.0;
                
                // Remove the element that's moving out of the window
                // Check which TreeSet contains the element to be removed
                if(!lo.remove(start)) hi.remove(start);
                
                // Move the window forward
                start++;
            }
        }
        return result;
    }
    
    // Main method with test cases
    public static void main(String[] args) {
        Solution solution = new Solution();
        
        // Test Case 1: Basic case with odd k
        // Expected: [2.0, 3.0, 4.0, 5.0, 6.0, 7.0]
        int[] nums1 = {1,2,3,4,5,6,7,8,9};
        int k1 = 3;
        System.out.println("Test Case 1 (k=3): " + 
                          java.util.Arrays.toString(solution.medianSlidingWindow(nums1, k1)));
        
        // Test Case 2: Basic case with even k
        // Expected: [2.5, 3.5, 4.5, 5.5, 6.5, 7.5]
        int[] nums2 = {1,2,3,4,5,6,7,8,9};
        int k2 = 4;
        System.out.println("Test Case 2 (k=4): " + 
                          java.util.Arrays.toString(solution.medianSlidingWindow(nums2, k2)));
        
        // Test Case 3: With duplicates
        // Expected: [1.0, 2.0, 2.0]
        int[] nums3 = {1,1,2,3,3};
        int k3 = 3;
        System.out.println("Test Case 3 (duplicates): " + 
                          java.util.Arrays.toString(solution.medianSlidingWindow(nums3, k3)));
        
        // Test Case 4: LeetCode example
        // Expected: [1.0, -1.0, -1.0, 3.0, 5.0, 6.0]
        int[] nums4 = {1,3,-1,-3,5,3,6,7};
        int k4 = 3;
        System.out.println("Test Case 4 (LeetCode example): " + 
                          java.util.Arrays.toString(solution.medianSlidingWindow(nums4, k4)));
    }
}






```
