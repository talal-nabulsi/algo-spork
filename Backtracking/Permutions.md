
# Permutations I (permuations of an array)

> Same exact solution as Permutations II


# Permuations II (permuations of an array, no dups)

> Same solution as string version


```java

     public List<List<Integer>> permuteUnique(int[] nums) {
        
        List<List<Integer>> res = new ArrayList<>();
        Map<Integer,Integer> map = new HashMap<>();
        
        for (int num : nums) 
            map.put(num, map.getOrDefault(num, 0) + 1);
        
        
        permute(map, res, new ArrayList<>(), nums.length);
        return res;
    }
    
    public void permute(Map<Integer, Integer> map, List<List<Integer>> res, List<Integer> temp, int len) {
        
        if (temp.size() == len) {
            res.add(new ArrayList<>(temp));
            return;
        }
        
        
        for (int num : map.keySet()) {
            int count = map.get(num);
            if (count != 0) {
                temp.add(num);
                map.put(num, map.get(num) - 1);
                permute(map, res, temp, len);
                map.put(num, map.get(num) + 1);
                temp.remove(temp.size() - 1);
            }
        }  
    }
```
