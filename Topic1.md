# Week 1 : Dynamic Programming

## The Framework Review

1. A function or data structure that will compute/contain the answer to the problem for every given state.
2. A recurrence relation to transition between states.
3. Base cases, so that our recurrence relation doesn't go on infinitely.

## 198. House Robber (Medium)
Forwards transition
```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        def dp(i):
            # Base cases
            if i == 0: 
                return nums[0]            
            if i == 1: 
                return max(nums[0], nums[1])            
            if i not in memo:
                memo[i] = max(dp(i - 1), dp(i - 2) + nums[i]) # Recurrence relation
            return memo[i]
        
        memo = {}
        return dp(len(nums) - 1)
```

## 746. Min Cost Climbing Stairs (Easy)
backwards transition
```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        def dp(i):
            if i==len(cost)-1:
                return cost[-1]
            if i==len(cost)-2:
                return cost[-2]
            
            if i not in memo:
                if i+1 not in memo:
                    memo[i+1]=dp(i+1)
                if i+2 not in memo:
                    memo[i+2]=dp(i+2)
                memo[i]=min(memo[i+1]+cost[i],memo[i+2]+cost[i])
            return memo[i]
        
        memo={}
        return min(dp(0),dp(1))
```

## 740. Delete and Earn
Define state as the maximum num in subsets and use count sort
```python
class Solution:
    def deleteAndEarn(self, nums: List[int]) -> int:
        points = defaultdict(int)
        max_number = 0
        # Precompute how many points we gain from taking an element
        for num in nums:
            points[num] += num
            max_number = max(max_number, num)

        @cache
        def max_points(num):
            # Check for base cases
            if num == 0:
                return 0
            if num == 1:
                return points[1]
            
            # Apply recurrence relation
            return max(max_points(num - 1), max_points(num - 2) + points[num])
        
        return max_points(max_number)
```
