# 979. Distribute Coins in Binary Tree (Median)
Bottom-up strategy with BFS or DFS implements

[BFS](#979.BFS)\
[DFS](#979.DFS)
# 3068. Find the Maximum Sum of Node Values (Hard)


## 979.BFS
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
## 979.DFS
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
