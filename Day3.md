# 979. Distribute Coins in Binary Tree (Median)
Bottom-up strategy with BFS or DFS implements

[Distribute Coins BFS](#distribute-coins-bfs)\
[Distribute Coins DFS](#distribute-coins-dfs)
# 3068. Find the Maximum Sum of Node Values (Hard)
First, we need to know the properties of the XOR operation

# 780. Reaching Points (Hard)
The key is to look backwards! \
Since one step back from the final completely matched situation, 
we can ensure that one item of ts, ty is still matched.\
[Reaching Points backwards](#reaching-points)


## Distribute Coins BFS
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def distributeCoins(self, root: Optional[TreeNode]) -> int:
        #bottom-up

        def move(node):
            lnode=node.left
            rnode=node.right

            if lnode:
                lmove=lnode.val-1
            else:
                lmove=0
            if rnode:
                rmove=rnode.val-1
            else:
                rmove=0

            node.val=node.val+lmove+rmove
            tot_move=abs(lmove)+abs(rmove)

            return tot_move


        # bfs
        queue=deque()
        queue1=deque()
        queue.append(root)
        queue1.append(root)
        while queue:
            node=queue.popleft()
            if node.right:
                queue.append(node.right)
                queue1.append(node.right)
            if node.left:
                queue.append(node.left)
                queue1.append(node.left)

        steps=0
        while queue1:
            node=queue1.pop()
            c=move(node)
            steps+=c

        return steps
```
## Distribute Coins DFS
```python
class Solution:
    def distributeCoins(self, root: Optional[TreeNode]) -> int:
        self.moves = 0

        def dfs(current):
            if current == None: return 0

            # Calculate the coins each subtree has available to exchange
            left_coins = dfs(current.left)
            right_coins = dfs(current.right)

            # Add the total number of exchanges to moves
            self.moves += abs(left_coins) + abs(right_coins)

            # The number of coins current has available to exchange
            return (current.val - 1) + left_coins + right_coins

        dfs(root)


        return self.moves
```

## Reaching Points
```python
class Solution:
    def reachingPoints(self, sx: int, sy: int, tx: int, ty: int) -> bool:
        while tx >= sx + ty or ty >= sy + tx:
            if tx > ty:
                tx = sx + (tx - sx) % ty
            else:
                ty = sy + (ty - sy) % tx

        return ty == sy and tx == sx

class Solution(object):
    def reachingPoints(self, sx, sy, tx, ty):
        while tx >= sx and ty >= sy:
            if tx == ty:
                break
            elif tx > ty:
                if ty > sy:
                    tx %= ty
                else:
                    return (tx - sx) % ty == 0
            else:
                if tx > sx:
                    ty %= tx
                else:
                    return (ty - sy) % tx == 0

        return tx == sx and ty == sy
```
