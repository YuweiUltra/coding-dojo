## 2750. Ways to Split Array Into Good Subarrays (Medium)
```python 
class Solution:
    def numberOfGoodSubarraySplits(self, nums: List[int]) -> int:
        cc=1
        c=0
        for i in range(len(nums)):
            if c==0 and nums[i]==1:
                c=1
            elif c>0 and nums[i]==0:
                c+=1
            elif c>0 and nums[i]==1:
                cc*=c
                c=1
        if c==0:
            return 0
        else:
            return int(cc%(10**9+7))
```
