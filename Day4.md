# 135. Candy (Hard)
- [Two pass](#candy-two-pass)
- [Up-Down-Peak Method](#candy-up-down-peak)

# 41. First Missing Positive (Hard)
1. Index as a Hash Key\
The idea is that for n length input nums, the first missing positive should be no larger than n+1.
So we can create a boolean array to store num in nums that is smaller than n+1. And using the Index as a Hash Key, update the boolean array
cost O(1) for every num.
2.  In-place Algorithms\
To save the storage space.

# 1863. Sum of All Subset XOR Totals (Easy)
We need to generate all possible subsets using backtracking. We can implement using DFS or BFS or biteise operation\
[Generate Subsets](#generate-subsets)



# Appendix Code
## Candy Two Pass
```python
class Solution:
    def candy(self, ratings: List[int]) -> int:
        if not ratings:
            return 0
        
        ret, up, down, peak = 1, 0, 0, 0
        
        for prev, curr in zip(ratings[:-1], ratings[1:]):
            if prev < curr:
                up, down, peak = up + 1, 0, up + 1
                ret += 1 + up
            elif prev == curr:
                up = down = peak = 0
                ret += 1
            else:
                up, down = 0, down + 1
                ret += 1 + down - int(peak >= down)
        
        return ret
```

## Candy Up Down Peak
```python
class Solution:
    def candy(self, ratings: List[int]) -> int:
        if not ratings:
            return 0
        
        ret, up, down, peak = 1, 0, 0, 0
        
        for prev, curr in zip(ratings[:-1], ratings[1:]):
            if prev < curr:
                up, down, peak = up + 1, 0, up + 1
                ret += 1 + up
            elif prev == curr:
                up = down = peak = 0
                ret += 1
            else:
                up, down = 0, down + 1
                ret += 1 + down - int(peak >= down)
        
        return ret
```

# Generate Subsets
```python
def subsets(nums):

    def backtrack(start=0, subset=[]):
        result.append(subset[:])
        for i in range(start, len(nums)):
            subset.append(nums[i])
            backtrack(i + 1, subset)
            subset.pop()
    
    result = []
    backtrack()
    return result

from collections import deque
def subsets(nums):
    result = [[]]
    for num in nums:
        queue = deque(result)
        for i in range(len(queue)):
            subset = queue.pop()
            new_subset = subset+[num]
            result.append(new_subset)   
    return result

# bitwise implement
def subsets(nums):
    result = []
    n = len(nums)
    
    # Generate all possible bitmasks
    for mask in range(2 ** n):
        subset = []
        for i in range(n):
            # If the i-th bit is set, include the element at index i
            if mask & (1 << i):
                subset.append(nums[i])
        result.append(subset)
    
    return result
```
