# 239. Sliding Window Maximum (Hard)

Review a little for the sort algorithm:
- find the maximum element O(n)
- find k-th largest element:
  1. QuickSelect Algorithm: This is a variation of the quicksort algorithm, which selects a pivot element and partitions the array around it. The algorithm can then recurse on the appropriate partition to find the k-th largest element. The average time complexity of this algorithm is O(n), but it has a worst-case time complexity of O(n^2) when the pivot is consistently chosen poorly.
  
  2. Heap-based Approach: Build a max-heap from the array in O(n) time. Then, extract the maximum element k-1 times, which takes O(k log n) time. The (k+1)-th extracted element is the k-th largest element in the original array. The overall time complexity is O(n + k log n).
  
  3. Counting Sort (if the range of values is small): Count the occurrences of each value, then iterate through the counts to find the k-th largest element. Time complexity is O(n + r), where r is the range of values in the array.
  
The answer for this question is very tricky. We use a `monotonic queue`.

- If the number increases, delete smaller ones from the left of the queue and add the number to the queue.
- If the number decreases, add it to the queue.

In this case, the monotonic queue contains indices of numbers that are monotonically decreasing.\
[Monotonic Queue](#monotonic-queue)

# 295. Find Median from Data Stream (Hard)

1. `Insertion Sort`:
Binary search for position to insert the new num O(logn) and conduct the instert operation O(n)

2. `Heaps (Priority Queues)`:\
Use two heaps: lo max-heap and hi min-heap.\
Define how to balance two heaps to keep their lengths close\
[Two Heap](#two-heap)

4. `Self-balancing Binary Search Trees` and `Multiset`:\
Since Self-balancing Binary Search Trees maintain height to a logarithmic bound. Thus inserting a new element has reasonably good time performance. \
Let's see the C++ version answer using STL std::multiset\
[Multiset](#multiset)

# 42. Trapping Rain Water (Hard)
- DP
- [Monotonic Queue](#trapping-rain-water-monotonic-queue)


# Appendix Code
## two side
```python
class Solution:
    def trap(self, height: List[int]) -> int:
        left_max=0
        right_max=0
        left_maxs={}
        right_maxs={}
        sums=0
        for i in range(1,len(height)-1):
            if height[i-1]>left_max:
                left_max=height[i-1]
            left_maxs[i]=left_max

        for i in range(len(height)-2,0,-1):
            if height[i+1]>right_max:
                right_max=height[i+1]
            right_maxs[i]=right_max

        for i in range(1,len(height)-1):
            x=min(left_maxs[i],right_maxs[i])-height[i]
            sums+=max(x,0)

        return sums
```
## Monotonic Queue
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

## Two Heap
```python
import heapq
class MedianFinder:

    def __init__(self):
        self.lo=[]
        self.hi=[]


    def addNum(self, num: int) -> None:
        if (not self.lo) and (not self.hi):
            self.lo.append(-num)
        else:
            m=self.findMedian()
            if num>=m:
                heapq.heappush(self.hi,num)
            else:
                heapq.heappush(self.lo,-num)

            self.balance()

    def balance(self):
        if len(self.hi)-len(self.lo)==2:
            num=heapq.heappop(self.hi)
            heapq.heappush(self.lo,-num)
        elif len(self.lo)-len(self.hi)==2:
            num=heapq.heappop(self.lo)
            heapq.heappush(self.hi,-num)


    def findMedian(self) -> float:
        if len(self.hi)>len(self.lo):
            return self.hi[0]
        elif len(self.hi)<len(self.lo):
            return -self.lo[0]
        else:
            return (-self.lo[0]+self.hi[0])/2

```
## Multiset
```c++
class MedianFinder {
    multiset<int> data;
    multiset<int>::iterator lo_median, hi_median;

public:
    MedianFinder()
        : lo_median(data.end())
        , hi_median(data.end())
    {
    }

    void addNum(int num)
    {
        const size_t n = data.size();   // store previous size

        data.insert(num);               // insert into multiset

        if (!n) {
            // no elements before, one element now
            lo_median = hi_median = data.begin();
        }
        else if (n & 1) {
            // odd size before (i.e. lo == hi), even size now (i.e. hi = lo + 1)

            if (num < *lo_median)       // num < lo
                lo_median--;
            else                        // num >= hi
                hi_median++;            // insertion at end of equal range
        }
        else {
            // even size before (i.e. hi = lo + 1), odd size now (i.e. lo == hi)

            if (num > *lo_median && num < *hi_median) {
                lo_median++;                    // num in between lo and hi
                hi_median--;
            }
            else if (num >= *hi_median)         // num inserted after hi
                lo_median++;
            else                                // num <= lo < hi
                lo_median = --hi_median;        // insertion at end of equal range spoils lo
        }
    }

    double findMedian()
    {
        return ((double) *lo_median + *hi_median) * 0.5;
    }
};
```
## Trapping Rain Water Monotonic Queue
```python
class Solution:
    def trap(self, height: List[int]) -> int:
        left_max=0
        right_queue=deque([2])
        for i in range(3,len(height)):
            if height[i]<height[right_queue[-1]]:
                right_queue.append(i)

            elif height[i]>=height[right_queue[-1]]:
                while right_queue and height[i]>=height[right_queue[-1]]:
                    right_queue.pop()
                right_queue.append(i)

    
        sum=0

        for i in range(1,len(height)-1):
            if height[i-1]>left_max:
                left_max=height[i-1]
            
            if i+1<=right_queue[0]:
                right_max=height[right_queue[0]]
            else:
                right_queue.popleft()
                right_max=height[right_queue[0]]
            
            x=min(left_max,right_max)
            sum+=(max(x-height[i],0))

        return sum
```
