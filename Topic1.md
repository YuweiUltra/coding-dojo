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
```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        @cache
        def dp(i, prev):
            if i < 0:
                return 0
            ans = dp(i - 1, False)
            if not prev:
                ans = max(ans, dp(i - 1, True) + nums[i])
                
            return ans
        
        return dp(len(nums) - 1, False)
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

## 740. Delete and Earn (Medium)
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

## 1770. Maximum Score from Performing Multiplication Operations (Hard)
```python
class Solution:
    def maximumScore(self, nums: List[int], multipliers: List[int]) -> int:
        n=len(multipliers)
        ln=len(nums)
        dp=[[0]*(n+1) for i in range(n+1)]

        for i in range(n+1):
            for j in range(i+1):
                if i==0:
                    dp[i][j]=0
                elif j==0:
                    dp[i][j]=dp[i-1][j]+multipliers[i-1]*nums[ln-i+j]
                else:
                    if i==j:
                        dp[i][j]=dp[i-1][j-1]+multipliers[i-1]*nums[j-1]
                    else:
                        dp[i][j]=max(dp[i-1][j-1]+multipliers[i-1]*nums[j-1],
                        dp[i-1][j]+multipliers[i-1]*nums[ln-i+j]
                        )
        return max(dp[-1])
```

## 1143. Longest Common Subsequence (Medium)
```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        m,n=len(text1),len(text2)
        dp=[[0 for _ in range(n+1)] for _ in range(m+1)]

        # i,j are the end pos(i,j cannot be used)
        for i in range(m+1):
            for j in range(n+1):
                if i==0 or j==0:
                    dp[i][j]=0
                else:
                    if text1[i-1]==text2[j-1]:
                        dp[i][j]=dp[i-1][j-1]+1
                    else:
                        dp[i][j]=max(dp[i-1][j],dp[i][j-1])
        return dp[m][n]
```

## 322. Coin Change (Medium)
```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        bignum=1e10
        @cache
        def dp(num):
            if num==0:
                return 0
            elif num in coins:
                return 1
            elif num<min(coins):
                return bignum
            else:
                m=bignum
                for i in coins:
                    m=min(m,dp(num-i)+1)
                return m
        
        if dp(amount)>=bignum:
            return -1
        else:
            return dp(amount)
```

## 518. Coin Change II (Medium)

```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        def numberOfWays(i: int, amount: int) -> int:
            if amount == 0:
                return 1
            if i == len(coins):
                return 0
            if memo[i][amount] != -1:
                return memo[i][amount]

            if coins[i] > amount:
                memo[i][amount] = numberOfWays(i + 1, amount)
            else:
                memo[i][amount] = numberOfWays(i, amount - coins[i]) + numberOfWays(i + 1, amount)
            
            return memo[i][amount]

        memo = [[-1] * (amount + 1) for _ in range(len(coins))]
        return numberOfWays(0, amount)
```
