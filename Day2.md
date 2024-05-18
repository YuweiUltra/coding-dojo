# 239. Sliding Window Maximum (hard)

Review a little for the sort algorithm:
- find the maximum element O(n)
- find k-th largest element:
  1. QuickSelect Algorithm: This is a variation of the quicksort algorithm, which selects a pivot element and partitions the array around it. The algorithm can then recurse on the appropriate partition to find the k-th largest element. The average time complexity of this algorithm is O(n), but it has a worst-case time complexity of O(n^2) when the pivot is consistently chosen poorly.
  
  2. Heap-based Approach: Build a max-heap from the array in O(n) time. Then, extract the maximum element k-1 times, which takes O(k log n) time. The (k+1)-th extracted element is the k-th largest element in the original array. The overall time complexity is O(n + k log n).
  
  3. Counting Sort (if the range of values is small): Count the occurrences of each value, then iterate through the counts to find the k-th largest element. Time complexity is O(n + r), where r is the range of values in the array.
  
The answer for this question is very tricky. We use a monotonic queue.

- If the number increases, delete smaller ones from the left of the queue and add the number to the queue.
- If the number decreases, add it to the queue.

In this case, the monotonic queue contains indices of numbers that are monotonically decreasing.


# 295. Find Median from Data Stream (hard)






## monotonic queue
```python

class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        # initilize
        assert k>=1 and len(nums)>=k

        queue=deque()
        queue.append(0)
        for i in range(1,k):
            if queue:
                if nums[i]>=nums[queue[0]]:
                    # pop all
                    queue=deque()
                    queue.append(i)
                elif nums[i]<nums[queue[-1]]:
                    queue.append(i)
                elif nums[i]>=nums[queue[-1]]:
                    while nums[i]>=nums[queue[-1]]:
                        queue.pop()
                    queue.append(i)
            else:
                queue.append(i)
        
        res=[]
        res.append(queue[0])

        for i in range(k,len(nums)):
            if i-(k-1)>queue[0]:
                queue.popleft()
            
            if queue:
                if nums[i]>=nums[queue[0]]:
                    # pop all
                    queue=deque()
                    queue.append(i)
                elif nums[i]<nums[queue[-1]]:
                    queue.append(i)
                elif nums[i]>=nums[queue[-1]]:
                    while nums[i]>=nums[queue[-1]]:
                        queue.pop()
                    queue.append(i)
            else:
                queue.append(i)

            res.append(queue[0])

        return [nums[i] for i in res]

```
