# Top k Frequent Elements
## https://leetcode.com/problems/top-k-frequent-elements

Given a non-empty array of integers, return the k most frequent elements.
```
Example 1:

Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]

Example 2:

Input: nums = [1], k = 1
Output: [1]
```
**Note:**

1. You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
2. Your algorithm's time complexity must be better than O(n log n), where n is the array's size.
3. It's guaranteed that the answer is unique, in other words the set of the top k frequent elements is unique.
4. You can return the answer in any order.


### Naive approach :
1. First create a map (Map<Integer,Integer>) for frequency (how many times individual numbers appear in the input aray).

2. Second step, reverse the map, so the frequency becomes the key and the value will be List<Integer> that appear that many times. (Use a TreeMap<Integer, List<Integer>>). Since we are intersted in the Top K elements using a TreeMap in second step, will give us the access to numbers with most frequency.    

3. Last step is to take the k elements from the TReeMap, since by default TreeMap sorts the keys in ascending order, we can use the lastEntry() method on reverse map.
    

# Implementation 
```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer,Integer> numToFreq = new HashMap<>();
        for(int num : nums) {
            int occurance = numToFreq.getOrDefault(num, 0);
            numToFreq.put(num, occurance + 1);
        }
        TreeMap<Integer, List<Integer>> freqToNumbers = new TreeMap<>();
        for(int key : numToFreq.keySet()) {
            freqToNumbers.putIfAbsent(numToFreq.get(key), new ArrayList<Integer>());
            freqToNumbers.get(numToFreq.get(key)).add(key);
        }
        // we are given that there will be atleast k distinct elements
        int[] res = new int[k];
        int index = 0;
        for(int i = 0; i < k; i++) {
            Map.Entry<Integer,List<Integer>> lastEntry = freqToNumbers.lastEntry();
            List<Integer> values = lastEntry.getValue();
            res[index++] = values.remove(0);
            if(values.size() == 0)
                freqToNumbers.remove(lastEntry.getKey());
        }
        return res;
    }
}
```
