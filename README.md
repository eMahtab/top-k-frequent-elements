# Top k Frequent Elements
## https://leetcode.com/problems/top-k-frequent-elements



# Implementation 
```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer,Integer> frequency = new HashMap<>();
        int[] result = new int[k];
        
        for(int num : nums) {
            frequency.put(num, frequency.getOrDefault(num, 0) + 1);
        }
        
        TreeMap<Integer, List<Integer>> freqToNum = new TreeMap<>();
        
        for(Integer key : frequency.keySet()) {
            freqToNum.putIfAbsent(frequency.get(key), new ArrayList<Integer>());
            freqToNum.get(frequency.get(key)).add(key);
        }
        
        int index = 0;
        while(index != k) {
            List<Integer> list  = freqToNum.lastEntry().getValue();
            result[index++] = list.get(0);
            list.remove(0);
            if(list.isEmpty())
               freqToNum.remove(freqToNum.lastEntry().getKey());
        }

       return result; 
    }
}
```
