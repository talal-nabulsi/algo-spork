

# Insert Interval, one of the easiest hard problems,lots of minor variations to solve.


## My OG solution


```java

public class Solution {
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
        
        List<Interval> result = new ArrayList<>();
        
        for (Interval interval : intervals) {
            
            if (newInterval == null || interval.end < newInterval.start) {
                result.add(interval);
            } else if (interval.start > newInterval.end) {
                result.add(newInterval);
                result.add(interval);
                newInterval = null;
            } else {
                newInterval.start = Math.min(newInterval.start, interval.start);
                newInterval.end = Math.max(newInterval.end, interval.end);
            }
            
        }
        
        if (newInterval != null) {
            result.add(newInterval);
        }
        
        return result;
    }
}

```

## Top Leetcode discussion solution


```java

public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
    List<Interval> result = new LinkedList<>();
    int i = 0;
    // add all the intervals ending before newInterval starts
    while (i < intervals.size() && intervals.get(i).end < newInterval.start)
        result.add(intervals.get(i++));
    // merge all overlapping intervals to one considering newInterval
    while (i < intervals.size() && intervals.get(i).start <= newInterval.end) {
        newInterval = new Interval( // we could mutate newInterval here also
                Math.min(newInterval.start, intervals.get(i).start),
                Math.max(newInterval.end, intervals.get(i).end));
        i++;
    }
    result.add(newInterval); // add the union of intervals we got
    // add all the rest
    while (i < intervals.size()) result.add(intervals.get(i++)); 
    return result;
}

```