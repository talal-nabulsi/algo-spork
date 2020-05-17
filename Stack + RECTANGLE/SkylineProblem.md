> Pretty easy problem, PriorityQueue/Heap is most optimal
> Probably a bit hard to engineer so you should memorize this one to get the cleanest code.

> Idea is to iterate through the points and put them in a heap. If max changes then we have a Critical Point!

> 1. Create elements from builidings that signifiy start/end
> 2. Sort elements (remember edge cases of matching building starts/ends)
> 3. Create Max PQ/Heap of Integer (no need for element) If the max changes when you insert height we have a Critical Point!
> 4. Start = add to heap, end = remove from heap

```java

class Solution {
    public List<int[]> getSkyline(int[][] buildings) {
        List<Element> elements = new ArrayList<>();
        for (int[] building : buildings) {
            Element start = new Element(building[0], building[2], true);
            Element end = new Element(building[1], building[2], false);
            elements.add(start);
            elements.add(end);
        }
        
        Collections.sort(elements);
        PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> b - a);

        pq.add(0); // remember to add zero as init
        List<int[]> res = new ArrayList<>();
        
        for (Element element : elements) {
            int max = pq.peek();
            if (element.start) pq.add(element.h);
            else pq.remove(element.h);
            
            if (pq.peek() != max) {
                if (element.start) res.add(new int[] {element.x, element.h});
                else res.add(new int[] {element.x, pq.peek()});   
            }   
        }
        return res;   
    }
    
    class Element implements Comparable<Element> {
        int x;
        int h;
        boolean start;
        
        public Element(int x, int h, boolean start) {
            this.x = x;
            this.h = h;
            this.start = start;
        }
        @Override
        public int compareTo(Element that) {
            if (this.x == that.x) {
                if (this.start && that.start) return that.h - this.h; // if starts match, bigger first
                if (!this.start && !that.start) return this.h - that.h; // if ends match, smaller first
                if (this.start != that.start) return this.start ? -1 : 1; //starts always go first
            }
            
            return this.x - that.x; 
        }
    }
}
```