## Python 3 Collections series: Set

### What is a set in python?

By definition in python a set is a collection of elements that adhere typically to a few guarantees:

- Objects stored in the set must be immutable, though the set itself is mutable
- Objects stored in the set must be hashable in order to achieve a sets duplication capabilities
- Sets are backed by hash tables in python, you should never rely on insertion order or the order in which elements in the set currently are. (There are also frozen and ordered sets which we will talk about later).


### Set instantiation and Gotchas!
In order to instantiate a set, we have a few methods available to us, but a few notes are important as there exist some edge cases that could sneak bugs into your code:

```python
simple_set = set(<iterable>) # This is an empty set
simple_set_with_values = {1,2,3,4,5} # This is a set with 1-5 integers
not_a_set = {} # Careful, this is not an empty set! it is infact a dictionary
set_comprehension = {number for number in range(10)} # Set comprehension
```

The set() vs {} method can be quite misleading, as strings in python are iterables, let's have a quick look at another gotcha when using the set() constructor.  When using the {} instantiation approach python will add the actual item into the set, when using set(iterable) it will add each item in the iterable.

```python
>>> word = 'word'
>>> worded_set = set(word)
>>> worded_set
{'w', 'd', 'o', 'r'} # Notice something here? there is no guarantee on the order of the elements!

-----------------------

>>> word_set_new = {word} # You would probably expect a similar set to the above?
>>> word_set_new
{'word'}
>>> len(word_set_new)
1 # Interesting, don't get caught out by this one!
```

By default a set in python 3 consumes a total of `224 bytes`, we can see this below:

```python
>>> from sys import getsizeof as size_it
>>> size_it(set())
224
```

Sets (compared to their list counter parts) are pretty memory hungry, we can see this outlined below:

```python
>>> values = range(250)
>>> type(values)
<class 'range'>
>>> len(values)
250
>>> size_it(list(values))
2360
>>> size_it(set(values))
8416  # So much bigger!
>>>
```


### Main uses of a Set:

One of the biggest benefits of the set is, erradicating duplicates:

```python
no_duplicates = set([1,2,3,4,5,5,5]) # Remember this is a single arg, list
no_other_duplicates = {'big', 'big', 'dog', 'dog'}

>>> no_duplicates
{1, 2, 3, 4, 5} # Notice the duplicate 5s are gone
>>> no_other_duplicates = {'big', 'big', 'dog', 'dog'}
>>> no_other_duplicates
{'dog', 'big'} # Notice the duplicate words are gone
```

One of the weirdest problems new set users come across is that they have customised objects, and they can add duplicate ones into the set just fine, the damn set must be broken!  Not quite; in order for a set to be able to actually figure out if you have a duplicate and where 'bucket' it should be in, you must implement at the very least two magic methods.  An overall example of this is outlined below:

```python
__hash__ : # hash should return an integer, objects which compare equal should have the same hash value.  If your class does not define a __eq__ it should NOT define a hash.

__eq__ : # your logic for determining how objects of your custom type should be considered 'equal'.  Python 3 is smart enough to provide a __ne__ for you, python 2 does not.

# a simple dog class
>>> class Dog:
...     def __init__(self, colour):
...             self.colour = colour
...

# Wait a minute, two of the same dogs are in my set!
>>> my_dogs = set([Dog('black'), Dog('black')])
>>> my_dogs
{<__main__.Dog object at 0x109c110b8>, <__main__.Dog object at 0x109deaeb8>}
```

As you can see, we have added two 'brown' dogs into a set just fine, these are as far as you are concerned, duplicates! set should only store one of them.  Let's try again by providing a __eq__ method for the Dog class:

```python
# a simple dog class
>>> class Dog:
...     def __init__(self, colour):
...             self.colour = colour
...
...     def __eq__(self, other):
...             return self.colour == other.colour
...
>>>
>>> dog_one = Dog('brown')
>>> dog_two = Dog('black')
>>> dog_three = Dog('brown')
>>>
>>> dog_one == dog_two
False
>>> dog_one == dog_three
True
>>>
>>> new_set = set([Dog('brown'), Dog('brown')]) # Uh oh, dog is not hashable!
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'Dog'
```

Again you can see, that dogs with the same hair are now considered 'equal' in your eyes, however the set collection still does not approve of your custom class, remember that magic method __hash__?  It's time we actually implemented it, so third time lucky:

```python
# a simple dog class
>>> class Dog:
...     def __init__(self, colour):
...             self.colour = colour
...
...     def __eq__(self, other):
...             return self.colour == other.colour
...		
...		# This is a good way to build a tuple of your attributes, for hashing
...     def __key(self):
...             return (self.colour)
...
...     def __hash__(self):
...             return hash(self.__key())
...
>>> cool_set = set([Dog('brown'), Dog('brown')])
>>> cool_set
{<__main__.Dog object at 0x109e227f0>} # Hooray! only 1 dog with brown hair is allowed in the set
>>>
```

### Truthness to set(s):
In general, an empty set will return `False` and a set with elements `True`:

```python
>>> z = set()
>>> bool(z)
False
>>> z or 'something_else'
'something_else'
>>> z and 'something_else?'
set()
>>>
```

### heterogeneous-ness:
Like pretty much everything in python, sets support heterogeneous types, this allows us to have things like this: (Again note: The order is not guaranteed!)

```python
>>> mixed_up = {1, 'two', Dog('brown')}
>>> mixed_up
{1, <__main__.Dog object at 0x109e22860>, 'two'}
>>>
```

### Immutability and sets
            
            









