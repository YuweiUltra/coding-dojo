## 460. LFU Cache (Hard)

- Object-Oriented Programming
- data structure



We want to manage the limited capacity cache. 
The Key operation is to remove lfu item in the cache for O(1).

My initial thought is to set the cache as a sorted list, 
with items ordered from left to right in decreasing use count, 
keeping the least frequently used (LFU) item at index -1. This way, 
we can easily remove the LFU item and add a new item. At the same time, we create
another dict to search easily in O(1).

[Link to LFU Cache False Example](#lfu-cache-false-example)

However, the problem is that in some cases (when every item wasn't used after being created), we need to switch adjacent items, which would take O(n) time. So, we can use a doubly linked list to move the tail item to the top in O(1) time.

[Link to LFU Cache doublylinkedlist Example](#lfu-cache-doublylinkedlist)

`OrderedDict` is implemented using a combination of a hash table and a doubly linked list. 

[Link to LFU Cache OrderedDict Example](#lfu-cache-ordereddict)



## LFU Cache False Example
```python
class counter:
    def __init__(self,key):
        self.key=key
        self.count=1
    
    def add_one(self):
        self.count+=1

class sort_counters:
    def __init__(self):
        # store counts both in list and dict
        # modify by key through dict and sort through list
        self.counts=[]
        self.counts_=dict()

    def add(self, key):
        new_counter=counter(key)
        self.counts.append(new_counter)
        self.counts_[key]=new_counter
        # move recent added to the left
        self.update(key)

    def update(self,key):
        # find counter
        update_counter=self.counts_[key]
        idx=self.counts.index(update_counter)
        
        while idx-1>=0:
            left_counter=self.counts[idx-1]
            # compare left_counter
            if left_counter.count>update_counter.count:
                break
            else:
                # switch the position of left_counter and update_counter
                self.counts[idx-1],self.counts[idx]=update_counter,left_counter
                idx-=1

class LFUCache:

    def __init__(self, capacity: int):
        self.capacity=capacity
        self.cache=dict()
        self.C=sort_counters()


    def get(self, key: int) -> int:
        if key in self.cache:
            self.C.counts_[key].add_one()
            self.C.update(key)
            return self.cache[key]
        else:
            return -1

    def reach_capacity(self):
        if len(self.cache)==self.capacity:
            return True
        else:
            return False

    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            self.cache[key]=value
            self.C.counts_[key].add_one()
            self.C.update(key)
        else:
            # check capcity
            if not self.reach_capacity():
                # add key and value
                self.cache[key]=value
                self.C.add(key)
            else:
                # remove lfu
                lfu_key=self.C.counts[-1].key
                del self.cache[lfu_key]
                del self.C.counts_[lfu_key]
                self.C.counts=self.C.counts[:-1]

                # add new key
                self.cache[key]=value
                self.C.add(key)

```

## LFU Cache Doublylinkedlist
```python
import collections

class Node:
    def __init__(self, key, val):
        self.key = key
        self.val = val
        self.freq = 1
        self.prev = self.next = None

class DLinkedList:
    """ An implementation of doubly linked list.
	
	Two APIs provided:
    
    append(node): append the node to the head of the linked list.
    pop(node=None): remove the referenced node. 
                    If None is given, remove the one from tail, which is the least recently used.
                    
    Both operation, apparently, are in O(1) complexity.
    """
    def __init__(self):
        self._sentinel = Node(None, None) # dummy node
        self._sentinel.next = self._sentinel.prev = self._sentinel
        self._size = 0
    
    def __len__(self):
        return self._size
    
    def append(self, node):
        node.next = self._sentinel.next
        node.prev = self._sentinel
        node.next.prev = node
        self._sentinel.next = node
        self._size += 1
    
    def pop(self, node=None):
        if self._size == 0:
            return
        
        if not node:
            node = self._sentinel.prev

        node.prev.next = node.next
        node.next.prev = node.prev
        self._size -= 1
        
        return node
        
class LFUCache:
    def __init__(self, capacity):
        """
        :type capacity: int
        
        Three things to maintain:
        
        1. a dict, named as `self._node`, for the reference of all nodes given key.
           That is, O(1) time to retrieve node given a key.
           
        2. Each frequency has a doubly linked list, store in `self._freq`, where key
           is the frequency, and value is an object of `DLinkedList`
        
        3. The min frequency through all nodes. We can maintain this in O(1) time, taking
           advantage of the fact that the frequency can only increment by 1. Use the following
		   two rules:
           
           Rule 1: Whenever we see the size of the DLinkedList of current min frequency is 0,
                   the min frequency must increment by 1.
           
           Rule 2: Whenever put in a new (key, value), the min frequency must 1 (the new node)
           
        """
        self._size = 0
        self._capacity = capacity
        
        self._node = dict() # key: Node
        self._freq = collections.defaultdict(DLinkedList)
        self._minfreq = 0
        
        
    def _update(self, node):
        """ 
        This is a helper function that used in the following two cases:
        
            1. when `get(key)` is called; and
            2. when `put(key, value)` is called and the key exists.
         
        The common point of these two cases is that:
        
            1. no new node comes in, and
            2. the node is visited one more times -> node.freq changed -> 
               thus the place of this node will change
        
        The logic of this function is:
        
            1. pop the node from the old DLinkedList (with freq `f`)
            2. append the node to new DLinkedList (with freq `f+1`)
            3. if old DlinkedList has size 0 and self._minfreq is `f`,
               update self._minfreq to `f+1`
        
        All of the above opeartions took O(1) time.
        """
        freq = node.freq
        
        self._freq[freq].pop(node)
        if self._minfreq == freq and not self._freq[freq]:
            self._minfreq += 1
        
        node.freq += 1
        freq = node.freq
        self._freq[freq].append(node)
    
    def get(self, key):
        """
        Through checking self._node[key], we can get the node in O(1) time.
        Just performs self._update, then we can return the value of node.
        
        :type key: int
        :rtype: int
        """
        if key not in self._node:
            return -1
        
        node = self._node[key]
        self._update(node)
        return node.val

    def put(self, key, value):
        """
        If `key` already exists in self._node, we do the same operations as `get`, except
        updating the node.val to new value.
        
        Otherwise, the following logic will be performed
        
        1. if the cache reaches its capacity, pop the least frequently used item. (*)
        2. add new node to self._node
        3. add new node to the DLinkedList with frequency 1
        4. reset self._minfreq to 1
        
        (*) How to pop the least frequently used item? Two facts:
        
        1. we maintain the self._minfreq, the minimum possible frequency in cache.
        2. All cache with the same frequency are stored as a DLinkedList, with
           recently used order (Always append at head)
          
        Consequence? ==> The tail of the DLinkedList with self._minfreq is the least
                         recently used one, pop it...
        
        :type key: int
        :type value: int
        :rtype: void
        """
        if self._capacity == 0:
            return
        
        if key in self._node:
            node = self._node[key]
            self._update(node)
            node.val = value
        else:
            if self._size == self._capacity:
                node = self._freq[self._minfreq].pop()
                del self._node[node.key]
                self._size -= 1
                
            node = Node(key, value)
            self._node[key] = node
            self._freq[1].append(node)
            self._minfreq = 1
            self._size += 1
```

## LFU Cache OrderedDict
```python
class LFUCache:

    def __init__(self, capacity: int):
        self.frequencies = defaultdict(lambda: OrderedDict())
        self.values = defaultdict(int)
        self.capacity = capacity
        self.minfreq = float('inf')
        
    def get(self, key: int) -> int:
        f = self.values[key]

        if not f: 
            del self.values[key]
            return -1
        
        self.frequencies[f+1][key] = self.frequencies[f][key]
        self.values[key] = f+1
        
        del self.frequencies[f][key]
        
        if self.minfreq == f and not len(self.frequencies[f]):
            self.minfreq = f+1
            
        return self.frequencies[f+1][key]

    def put(self, key: int, value: int) -> None:
        if not self.capacity: return      
        
        if len(self.values) == self.capacity: 
            if not self.values[key]:
                k = self.frequencies[self.minfreq].popitem(last=False)
                del self.values[k[0]] 
                
        f = self.values[key]
        self.values[key] += 1
        
        if f != 0:
            self.frequencies[f+1][key] = value
            del self.frequencies[f][key]
            
            if self.minfreq == f and not len(self.frequencies[f]):
                self.minfreq = f+1
        else: 
            self.frequencies[f+1][key] = value    
        
        self.minfreq = min(self.values[key], self.minfreq)
```


    
