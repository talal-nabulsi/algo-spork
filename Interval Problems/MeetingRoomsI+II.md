# Meeting Rooms I

> Trivial overlap


```java

   public boolean canAttendMeetings(Interval[] intervals) {
        
        Arrays.sort(intervals, new MeetingSorter());
        
        for (int i = 0; i < intervals.length - 1; i++) 
            if (intervals[i].end > intervals[i + 1].start) return false;

        return true;
    }
```


# Meeting Rooms II

> Two different solutions, sort start and end times and heap!
> Kinda like heap tbh, but first one is nice

```java

class Solution {
    
    // Minimum Meeting Rooms II
    // Two main solutions you can use: PriorityQueue and Sorting Start/End times, 2nd one tends to be better!!!!
    public int minMeetingRooms(int[][] intervals) {
        
        int maxRooms = 0;
        int rooms = 0;
        
        int starts[] = new int[intervals.length];
        int ends[] = new int[intervals.length];
        
        for (int i = 0; i < intervals.length; i++) {        
            starts[i] = intervals[i][0];
            ends[i] = intervals[i][1];
        }
        
        Arrays.sort(starts);
        Arrays.sort(ends);
        int i = 0;
        int j = 0;
        
        int max = 0;
        
        // Pretty Easy, when you start a meeting increase a room, end meeting = decrease rooms
        while (i < starts.length && j < ends.length) {
            if (starts[i] < ends[j]) {
                rooms++;
                i++;
                max = Math.max(max, rooms);
            } else {
                rooms--;
                j++;
            }            
            
        }
        
        return max;
        
    }
}

```

## The Heap Solution (Very simple logic)

> Idea: Min heap by END times, that way the top of the heap is the meeting that is ending the earliest

> When we add a new meeting, check the top of the heap, if no overlap we can kick out the old meeting and replace it, else we need a new meeting

```java

// Heap Solution (my modification of leetcode sol to make more sense)
public int minMeetingRooms2(int[][] intervals) {
    if (intervals == null || intervals.length == 0) return 0;
        
    // Sort the intervals by start time
    Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
    
    // Use a min heap to track the minimum end time of merged intervals, so that way we pop whichever finishes earliest
    PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
    
    // start with the first meeting, put it to a meeting room
    pq.offer(intervals[0]);
    
    for (int i = 1; i < intervals.length; i++) {
        // get the meeting room that finishes earliest
        int[] interval = pq.peek();
        
        // if the current meeting starts after (no overlap)
        // there's no need for a new room, kick out that meeting and replace it
        if (intervals[i][0] >= interval[1])             
            pq.poll();      
        
        pq.offer(intervals[i]);
    }
    
    return pq.size();
}
    
```