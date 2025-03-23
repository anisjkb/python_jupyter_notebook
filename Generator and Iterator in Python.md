# Generator and Iterator in Python
---
## 1. Generator:
A generator in Python is a special type of iterator that allows you to iterate over a sequence of values lazily, meaning it generates values one at a time as they are needed, rather than storing the entire sequence in memory. This makes generators very memory-efficient for handling large datasets or infinite sequences.

### Key Features of Generators:
1. **Defined Using `yield`:** Instead of `return`, generators use the `yield` keyword to produce values. When a `yield` statement is encountered, the function's state is saved, and the value is returned to the caller.
2. **Resume Execution:** When the generator is called again, it resumes execution from where it left off, maintaining the state of its variables.
3. **Memory-Efficient:** Unlike lists, generators do not store all values in memory at once, which is ideal for handling large data.
4. **Finite or Infinite:** They can generate a finite sequence or continue indefinitely.

### How to Create and Use a Generator:
Here’s example that demonstrates the use of a generator:

**Example-1:** Define a generator function to yield even numbers up to a given limit

```python
# Way-1: Define a generator function to yield even numbers

def even_numbers_generator(limit): # param limit: The maximum number to check for even numbers.
    for num in range(limit + 1):
        if num % 2 == 0:
            yield num
   
# Use the generator
even_gen = even_numbers_generator(10)  # Generate even numbers up to 10 (exclusive)

# Iterate through the generator and print each even number
for even in even_gen:
    print(even)

# Way-2: Define a generator function to yield even numbers

def even_numbers(limit):
    for num in range(0, limit, 2):  # Start from 0, step by 2
        yield num

# Use the generator
even_gen = even_numbers(10)  # Generate even numbers up to 10 (exclusive)

# Iterate through the generator and print each even number
for even in even_gen:
    print(even)
```
**Output:**
```
0
2
4
6
8
10
```
### Explanation of the Example-1:
1. **Generator Function:** `even_numbers(limit)` is a generator that uses `yield` to produce even numbers one by one up to the specified `limit`.
2. **Range with Step:** The `range()` function is used with a step of 2 to generate even numbers efficiently.
3. **Iteration:** When iterating through the generator, it calculates and returns each even number on demand.

**Example-2:** Generate Fibonacci numbers less than 10

```python
# Define a generator function
def fibonacci_generator(limit):
    a, b = 0, 1
    while a < limit:
        yield a  # Produces the next Fibonacci number
        a, b = b, a + b  # Update values for the next iteration

# Use the generator
fibonacci = fibonacci_generator(10)  # Generate Fibonacci numbers less than 10

# Iterate through the generator
for num in fibonacci:
    print(num)
```
**Output:**
```
0
1
1
2
3
5
8
```

### Explanation of the Example-2:
1. **Generator Function:** `fibonacci_generator()` is a generator function that uses `yield` to produce Fibonacci numbers.
2. **State Preservation:** Each time `yield` is executed, the function pauses, and its state is saved.
3. **Iteration:** When you loop through the generator (`for num in fibonacci`), it resumes execution from the last `yield` statement, calculates the next Fibonacci number, and yields it again.


### Why Use Generators?
- **Efficiency:** When working with large datasets, generators consume less memory.
- **Pipelines:** Generators are useful for creating data pipelines where one generator feeds another.

---
## 2. Iterator

In Python, an **iterator** is an object that enables you to traverse through a collection (e.g., a list, tuple, dictionary, or set) one element at a time. It implements two main methods: 

1. **`__iter__()`**: This returns the iterator object itself.
2. **`__next__()`**: This returns the next value in the sequence. When there are no more items to return, it raises a `StopIteration` exception.

### How Iterators Work
Think of an iterator as a bookmark that remembers where you are in a collection. Unlike a loop that automatically handles iteration, iterators allow you to control the flow manually.

### Example of an Iterator
Here’s an example to explain iterators in Python:

```python
# Example of an iterator
my_list = [1, 2, 3, 4]

# Get an iterator object from the list
iterator = iter(my_list)

# Access items using the iterator
print(next(iterator))  # Output: 1
print(next(iterator))  # Output: 2
print(next(iterator))  # Output: 3
print(next(iterator))  # Output: 4

# If you call `next` again, it will raise StopIteration
```

### Iterators vs Iterables
- An **iterable** is an object that can return an iterator (e.g., lists, tuples, strings). You can get an iterator from an iterable by calling the built-in `iter()` function.
- An **iterator**, on the other hand, is an object with a state that remembers its position during iteration. It can be used with the `next()` function to fetch items.

### Custom Iterators
You can create your own iterators by defining a class that implements the `__iter__()` and `__next__()` methods. Here’s an example:

```python
class Count:
    def __init__(self, limit):
        self.limit = limit
        self.current = 0

    def __iter__(self):
        return self  # The iterator object is returned

    def __next__(self):
        if self.current < self.limit:
            self.current += 1
            return self.current
        else:
            raise StopIteration  # End of iteration

# Using the custom iterator
counter = Count(5)
for number in counter:
    print(number)
```

**Output:**
```
1
2
3
4
5
```

### Key Points
- Iterators are very memory-efficient, as they do not require creating a full collection in memory.
- They're useful when processing large data streams or files.
- Iterators allow greater control over data flow compared to `for` loops.
