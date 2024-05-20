## 4. Median of Two Sorted Arrays (Hard)

1. Merge Sort  O(n)
2. [Binary Search](#binary-search) O(logn)\
Transfer the problem into find the Kth smallest value. If len(n+m) is even, we need to find twice.\
- By comparing the mid values of two sorted list, we can remove binary parts that are
defintly bigger or smaller (depends on the relation of K and len(n+m)/2) than the Kth smallest value and also update the k value.
- Write binary serching function and recusively utilize it. The marginal condition is one array is empty, Then
just return the corresponding element in the other array.

## 1041. Robot Bounded In Circle (Medium)
Perform instructions until the Robot head to North direction again and compare the position with original position.\
If the position changes, than return False.

[Bounded In Circle](#bounded-in-circle)

## 1328. Break a Palindrome (Medium)
[Greedy](#greedy)


## Binary Search
```python
class Solution:
    def findMedianSortedArrays(self, A: List[int], B: List[int]) -> float:
        na, nb = len(A), len(B)
        n = na + nb

        def solve(k, a_start, a_end, b_start, b_end):
            # If the segment of on array is empty, it means we have passed all
            # its element, just return the corresponding element in the other array.
            if a_start > a_end:
                return B[k - a_start]
            if b_start > b_end:
                return A[k - b_start]

            # Get the middle indexes and middle values of A and B.
            a_index, b_index = (a_start + a_end) // 2, (b_start + b_end) // 2
            a_value, b_value = A[a_index], B[b_index]

            # If k is in the right half of A + B, remove the smaller left half.
            if a_index + b_index < k:
                if a_value > b_value:
                    return solve(k, a_start, a_end, b_index + 1, b_end)
                else:
                    return solve(k, a_index + 1, a_end, b_start, b_end)
            # Otherwise, remove the larger right half.
            else:
                if a_value > b_value:
                    return solve(k, a_start, a_index - 1, b_start, b_end)
                else:
                    return solve(k, a_start, a_end, b_start, b_index - 1)

        if n % 2:
            return solve(n // 2, 0, na - 1, 0, nb - 1)
        else:
            return (
                solve(n // 2 - 1, 0, na - 1, 0, nb - 1)
                + solve(n // 2, 0, na - 1, 0, nb - 1)
            ) / 2
```

## Bounded In Circle
```python
class Solution:
    def isRobotBounded(self, instructions: str) -> bool:
        class D:
            N=(0,1)
            S=(0,-1)
            E=(1,0)
            W=(-1,0)

        D_list=[D.N,D.E,D.S,D.W]

        def perform(instructions,x,y,d):
            for i in instructions:
                if i=="G":
                    x=x+d[0]
                    y=y+d[1]
                if i=="R":
                    i=D_list.index(d)
                    next_i=0 if i==3 else i+1
                    d=D_list[next_i]
                if i=="L":
                    i=D_list.index(d)
                    next_i=3 if i==0 else i-1
                    d=D_list[next_i]
            return x,y,d
        
        x=y=0
        d=D.N
        x,y,d=perform(instructions,x,y,d)
        while d!=D.N:
            x,y,d=perform(instructions,x,y,d)
        
        if x==0 and y==0:
            return True
        else:
            return False
```

## Greedy
```python
class Solution:
    def breakPalindrome(self, palindrome: str) -> str:
        if len(palindrome)==1:
            return ""
        
        n=len(palindrome)
        strl=list(palindrome)
        if n%2==1:
            left=palindrome[:(n-1)//2]
        else:
            left=palindrome[:n//2]

        for index,i in enumerate(left):
            if i !="a":
                strl[index]="a"
                return "".join(strl)

        strl[-1]="b"
        return "".join(strl)
```
