# namedtuple()

Named tuples assign meaning to each position in a tuple. Add the ability to access fields by name instead of position index.

```python
collections.namedtuple(typename, field_names, *, rename=False, defaults=None, module=None)
```
- return a new tuple subclass named *typename*
- \_\_repr__(): a method which lists the tuple contentss in a ``name=value`` format.
- *field_names*: a sequence of strings such as `['x','y']`. Also can be a single string with each field_name separated by whitespace and/or commas `'x y'` or `'x, y'`.
	- don't start with underscore or digit, and cannot be a keyword.
- if *rename* is True, invalid fieldnames are automatically replaced with positional names. For example, `['abc', 'def', 'ghi', 'abc']` is converted to `['abc', '_1', 'ghi', '_3']`
- _defaults_ can be `None` or an iterable of default values. Since fields with a default value must come after any fields without a default, the _defaults_ are applied to the rightmost parameters. For example, if the fieldnames are `['x', 'y', 'z']` and the defaults are `(1, 2)`, then `x` will be a required argument, `y` will default to `1`, and `z` will default to `2`.
- If *module* is defined, the \_\_module__ attribute od the named tuple is set to that value.

## Example
```python
>>> # Basic example
>>> Point = namedtuple('Point', ['x', 'y'])
>>> p = Point(11, y=22)     # instantiate with positional or keyword arguments
>>> p[0] + p[1]             # indexable like the plain tuple (11, 22)
33
>>> x, y = p                # unpack like a regular tuple
>>> x, y
(11, 22)
>>> p.x + p.y               # fields also accessible by name
33
>>> p                       # readable __repr__ with a name=value style
Point(x=11, y=22)
```

## Methods
```python
somenamedtuple._make(iterable) #or sequence
._asdict() # return a dict which maps field names tot heir corresponding values
._replace(**kwargs) # return a nre instance of the named tuple replacing specifiec fields with new values
#**kwargs: field_name=new_value
_fields #tuple of strings listing field names
_field_defaults #dictionary mapping field names to default values
namedtuple(**dict) #to convert a dictionary to a named tuple
Point3D = namedtuple('Point3D', Point._fields + ('z',)) #to add a new field
```
# deque
```python
class collections.deque([iterable[, maxlen]])
```
- returns a new deque object initialized left-to-right with data from *iterable*. If *iterable* is not specified, the new deque is empty.
- O(1) performance to append and pop from either side of deque
- *max_len* is not specified or is None, may grow to an arbitrary length.
	- Once a bounded length deque is full, when new items are added, a corresponding number of items are discarded.
## Methods
```python
append(x) #add x to the right
appendleft(x)
clear() #remove all elements
copy() #create a shallow copy of the deque
count(x) #the number of deque elements equal to x
extend(iterable) #extend the right side by appending
extendleft(iterable) #note, series of left appends results in reversing
index(x[, start[, stop]]) #position of x in the deque(at or after index start and before index stop). Return first match or ValueError
insert(i,x)# insert x at position i. if the insertion cause a bounded deque, and IndexError is raised
pop() #remove and return from right side or IndexError
popleft()
remove(value)#remove first occurrence
reverse()#reverse the elements
rotate(n=1)#rotate the deque n steps to the right. if n is negative, rotate to the left
```

It´s possible to implement deque slicing and deletion with rotate and pop. Also is easy to implement dup, drop, swap, over, pick, rot, and roll.
# ChainMap

# Counter
# OrderedDict
# defaultDict
# UserDict
# UserList
# UserString
