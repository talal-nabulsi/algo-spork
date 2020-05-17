
# Merge Intervals


> Also a trivial problem

```java

  public List<Interval> merge(List<Interval> intervals) {
        
        Collections.sort(intervals, new IntervalComparator()); // sort intervals by start date
        List<Interval> result = new ArrayList<>();
        
        for (Interval interval : intervals) {
            
            if (result.size() == 0 || result.get(result.size() - 1).end < interval.start) {
                result.add(interval); //no need to merge
            } else {
                result.get(result.size() - 1).end = Math.max(interval.end, result.get(result.size() - 1).end); //merge intervals
            }
        }
        
        return result;
        
    }


```


> Facebook Follow-Up
Question: How do you add intervals and merge them for a large stream of intervals? 

?? TBD