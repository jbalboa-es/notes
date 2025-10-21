# Chapter 1
## Useful
```python
sum(list)
len(list/dict)
line.split('char_to_split')

```
## 1.1 Unpacking a Sequence into Separate Variables
- Requirement: Number of variables and structure match the sequence.
- \_ to discard
## 1.2 Unpacking Elements from Iterables of Arbitrary Length
- *star expression*:
``` python
first, *middle, last = grades
return avg(middle)

#starred variable store a List
```
- throwaway variable name
	- \_
	- *ign* (ignored)
- can use starred variable as the arguments of a function, they'll separate each element of the list.
## 1.3 Keeping the Last N Items
```python
from collections import deque
def search(lines, pattern, history=5):
	previous_lines=deque(maxlen=history)
	...
	
# adding or popping from a deque has O(1) complexity
```
## 1.4 Finding the Largest or Smallest N Items
```python
import heapq
heapq.nlargest(n, list) #nsmallest
cheap = heapq.nsmallest(3, portfolio, key=lambda s:s['price']) #allows to use with more complicated data structures
heap.heapify(list) #to convert the list to a heap
heap.heappop(heap) #O(logN) to find smallest item and pops off
```
## 1.5 Implementing a Priority Queue
- heapq
- create a PriorityQueue class with heappush() and heappop()
## 1.6 Mapping Keys to Multiple Values in a Dictionary
- If you want to map keys to multiple values, you need to store the multiple values in another container such as a list or set
```python
from collections import defaultdict
#automatically initializes the first value so you can simly focus on adding items
d = defaultdict(list)
d = defaultdict(set)
```
## 1.7 Keeping Dictionaries in Order
```python
from collections import OrderedDict
```