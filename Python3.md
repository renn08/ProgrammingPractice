# Python3

1. id() returns the address of an object.

2. == can be used to array element-wise comparison.

3. ord() returns the Unicode point for a char.

4. collections.Counter(): https://docs.python.org/3/library/collections.html#collections.Counter
   Treat missing element as zero count, so Counter(a=3) == Counter(a=3, b=0) returns true.

5. self.visited = [false for _ in range(n)] # _ is the thrownaway variable that itself won't be used 

6. There's no python max heap inplementation, one can use inverse value min pq and inverse again when poping to do so. heapq can work on []. heapq uses binary heap algorithm doing in-place on data while priorityQueue uses mutex and slower. Recall heap sort alg: https://www.geeksforgeeks.org/heap-sort/, heapify(recursively make a tree rooted at i binary heap): at i, compare with child node of i and float largest up, this make sure i is larger than its child, but swap might break child tree invariant thus continue heapify on swapped up original pos child node. And then we do heapify from end to start of array, (only need to start from half pos and continue to first since later node are leaf nodes) and we fix invariant along the way if smaller go down. Then we get a whole tree as a binary max heap. Then we do sorting: take out max, and try to heapify from begin again but we have no node at begin so we take one leaf node (won't break invariant since this node has no child) to place at root and do heapify. And we get a bianry heap again, we do the process again and again until all nodes were taken and we sorted the array.

7. Python unordered_set is just set([a]) using add to add element (implenmented as hash table). Python set (ordered) is collections.OrderedSet or collections.OrderedDict (is implemented as a double linked list)

   ```python
   from collections import OrderedDict
   
   # Creating an ordered set-like structure
   ordered_set = OrderedDict.fromkeys([1, 2, 3, 4, 5])
   
   # Adding an element
   ordered_set[6] = None
   
   # Removing an element
   del ordered_set[3]
   
   # Checking membership
   if 4 in ordered_set:
       print("4 is in the ordered set")
   
   # Iterating through the ordered set
   for element in ordered_set:
       print(element)
   
   ```

   ```python
   from sortedcontainers import SortedSet
   
   # Creating a SortedSet
   sorted_set = SortedSet([3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5])
   
   # Adding an element
   sorted_set.add(8)
   
   # Removing an element
   sorted_set.discard(5)
   
   # Checking membership
   if 4 in sorted_set:
       print("4 is in the sorted set")
   
   # Iterating through the sorted set
   for element in sorted_set:
       print(element)
   
   ```

   8. Python queue: https://www.geeksforgeeks.org/queue-in-python/ can use duque()

   9. python is check object identity while == check for equality of values.

   10. Python iter():

       ```python
       my_string = "Hello"
       my_iterator = iter(my_string)
       
       for char in my_iterator:
           print(char)
       ```

       

       ```python
       # list of vowels
       phones = ['apple', 'samsung', 'oneplus']
       phones_iter = iter(phones)
       
       print(next(phones_iter))   
       print(next(phones_iter))    
       print(next(phones_iter))    
       
       # Output:
       # apple
       # samsung
       # oneplus
       ```

11. Python collections.defaultdict can treat missed key a default value need to define the type of value for example a = defaultdict(int)

12. python sort

    In Python, you can use the `sorted()` function to sort various types of iterables, including lists, tuples, and strings. The `sorted()` function returns a new sorted list, and it does not modify the original iterable. If you want to sort a list in-place, you can use the `sort()` method of the list.

    Here are some examples:

    ### Sorting a List:

    ```
    pythonCopy code
    # Sorting a list
    original_list = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5]
    sorted_list = sorted(original_list)
    
    print("Original list:", original_list)
    print("Sorted list:", sorted_list)
    ```

    ### Sorting a Tuple:

    ```
    pythonCopy code
    # Sorting a tuple
    original_tuple = (3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5)
    sorted_tuple = tuple(sorted(original_tuple))
    
    print("Original tuple:", original_tuple)
    print("Sorted tuple:", sorted_tuple)
    ```

    ### Sorting a String:

    ```
    pythonCopy code
    # Sorting a string
    original_string = "hello"
    sorted_string = ''.join(sorted(original_string))
    
    print("Original string:", original_string)
    print("Sorted string:", sorted_string)
    ```

    ### In-Place Sorting a List:

    ```
    pythonCopy code
    # In-place sorting a list
    numbers = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5]
    numbers.sort()
    
    print("Sorted list in-place:", numbers)
    ```

    Remember that the `sorted()` function and the `sort()` method use the default ordering for the data type. If you have a more complex data structure or want to customize the sorting order, you can use the `key` parameter with a custom sorting function.

    ```
    pythonCopy code
    # Custom sorting with a key function
    words = ["apple", "banana", "cherry", "date"]
    sorted_words = sorted(words, key=lambda x: len(x))
    
    print("Original words:", words)
    print("Sorted words by length:", sorted_words)
    ```

13. In Python string and tuple is immutable, cannot be changed inside, if need modify need to create a new one. (so can be hashable and serve as key in dict)

14. Python enumerate: 

15. In Python, the `enumerate` function is a built-in function that is used to iterate over a sequence (such as a list, tuple, or string) while keeping track of the index of the current item. It returns pairs of the form `(index, element)`.

    Here's a basic example of how `enumerate` is used:

    ```
    pythonCopy code
    my_list = ['apple', 'banana', 'cherry']
    
    for index, value in enumerate(my_list):
        print(f"Index: {index}, Value: {value}")
    ```

    This would output:

    ```
    yamlCopy code
    Index: 0, Value: apple
    Index: 1, Value: banana
    Index: 2, Value: cherry
    ```

    You can also specify a start index for enumeration:

    ```
    pythonCopy code
    my_list = ['apple', 'banana', 'cherry']
    
    for index, value in enumerate(my_list, start=1):
        print(f"Index: {index}, Value: {value}")
    ```

    This would output:

    ```
    yamlCopy code
    Index: 1, Value: apple
    Index: 2, Value: banana
    Index: 3, Value: cherry
    ```

    In addition to lists, `enumerate` can be used with other iterable objects like tuples or strings.

    Here's an example with a string:

    ```
    pythonCopy code
    my_string = "Hello"
    
    for index, char in enumerate(my_string):
        print(f"Index: {index}, Character: {char}")
    ```

    This would output:

    ```
    yamlCopy code
    Index: 0, Character: H
    Index: 1, Character: e
    Index: 2, Character: l
    Index: 3, Character: l
    Index: 4, Character: o
    ```

    `enumerate` is often used in loops where you need both the index and the value of each item in the iterable.

    14. Python zip

The `zip` function in Python is used to combine two or more iterables element-wise. It returns an iterator that generates tuples containing elements from the input iterables. Here's a basic example:

```python
pythonCopy code
list1 = [1, 2, 3]
list2 = ['a', 'b', 'c']

zipped = zip(list1, list2)

# Convert the zip object to a list for easier printing
result = list(zipped)

print(result)
```

This would output:

```python
cssCopy code
[(1, 'a'), (2, 'b'), (3, 'c')]
```

If the input iterables are of different lengths, `zip` stops creating tuples when the shortest input iterable is exhausted.

You can also use `zip` with more than two iterables:

```python
pythonCopy code
list1 = [1, 2, 3]
list2 = ['a', 'b', 'c']
list3 = ['x', 'y', 'z']

zipped = zip(list1, list2, list3)

result = list(zipped)

print(result)
```

This would output:

```python
cssCopy code
[(1, 'a', 'x'), (2, 'b', 'y'), (3, 'c', 'z')]
```

`zip` is often used in conjunction with `for` loops to iterate over multiple iterables simultaneously:

```python
pythonCopy code
list1 = [1, 2, 3]
list2 = ['a', 'b', 'c']

for item1, item2 in zip(list1, list2):
    print(f"Item from list1: {item1}, Item from list2: {item2}")
```

This would output:

```python
csharpCopy code
Item from list1: 1, Item from list2: a
Item from list1: 2, Item from list2: b
Item from list1: 3, Item from list2: c
```



15. Python find and find: https://www.toppr.com/guides/python-guide/references/methods-and-functions/methods/string/rfind/python-string-rfind/#:~:text=16%2024%20%2D1-,Difference%20between%20find()%20and%20rfind(),i.e.%20the%20very%20first%20index.

    Definition

    - ***Python rfind() function\*** *is used to return the highest index value of the last occurrence of the substring from the input string; else it returns -1.*
    - *The **Python rfind()** is an in-built string method that returns the index position of the character if found; else it returns value -1.*

    ## Python rfind() Syntax

    Python rfind() function follows the below-mentioned syntax:

    

    ```python
    string.rfind(substr, start, end)
    
                    
    ```

    **Note** – The rfind() function is case-sensitive.

16. string.ascii_lowercase and string.ascii_uppercase to represent lowercase and uppercase chars

17. Python3 can use type hints (useful for developers) such as res: List[str]

18. Python3 has reversed(arr) and arr.reverse() just like sorted() and sort(), and if want to sort or reverse a range of elem in arr, have to use sorted() and reversed() and use slicing: arr[1:3] = reversed(arr[1:3]) for example.

19. in range(3,-1,-1) last is step, second is end (exclusive)

20. swap in python can do a, b = b, a

21. python / will always return a float number

22. Python set methods: 

23. 
    In addition to the `add()` method, sets in Python have several other methods for common set operations. Here are some of the key methods:

    1. **`add(element)`**: Adds an element to the set. If the element is already present, this operation has no effect.

       ```
       pythonCopy code
       my_set = {1, 2, 3}
       my_set.add(4)
       print(my_set)  # Output: {1, 2, 3, 4}
       ```

    2. **`remove(element)`**: Removes the specified element from the set. If the element is not present, it raises a `KeyError`.

       ```
       pythonCopy code
       my_set = {1, 2, 3, 4}
       my_set.remove(3)
       print(my_set)  # Output: {1, 2, 4}
       ```

    3. **`discard(element)`**: Removes the specified element from the set if it is present. If the element is not present, this operation has no effect.

       ```
       pythonCopy code
       my_set = {1, 2, 3, 4}
       my_set.discard(3)
       print(my_set)  # Output: {1, 2, 4}
       ```

    4. **`pop()`**: Removes and returns an arbitrary element from the set. If the set is empty, it raises a `KeyError`.

       ```
       pythonCopy code
       my_set = {1, 2, 3, 4}
       popped_element = my_set.pop()
       print(popped_element)  # Output: (some element, not deterministic)
       ```

    5. **`clear()`**: Removes all elements from the set, making it an empty set.

       ```
       pythonCopy code
       my_set = {1, 2, 3, 4}
       my_set.clear()
       print(my_set)  # Output: set()
       ```

    6. **`union(other_set)` or `|` operator**: Returns a new set containing all unique elements from both sets.

       ```
       pythonCopy code
       set1 = {1, 2, 3}
       set2 = {3, 4, 5}
       union_set = set1.union(set2)
       # Alternatively: union_set = set1 | set2
       print(union_set)  # Output: {1, 2, 3, 4, 5}
       ```

    7. **`intersection(other_set)` or `&` operator**: Returns a new set containing the common elements between two sets.

       ```
       pythonCopy code
       set1 = {1, 2, 3}
       set2 = {3, 4, 5}
       intersection_set = set1.intersection(set2)
       # Alternatively: intersection_set = set1 & set2
       print(intersection_set)  # Output: {3}
       ```

    8. **`difference(other_set)` or `-` operator**: Returns a new set containing the elements that are in the first set but not in the second set.

       ```
       pythonCopy code
       set1 = {1, 2, 3}
       set2 = {3, 4, 5}
       difference_set = set1.difference(set2)
       # Alternatively: difference_set = set1 - set2
       print(difference_set)  # Output: {1, 2}
       ```

    These are some of the fundamental methods for working with sets in Python. Depending on your specific use case, you might also encounter additional set methods or use other set operations.

    

    24. In the context of programming, serialization refers to the process of converting an object or data structure into a format that can be easily stored, transmitted, or reconstructed. The resulting data can be in a text or binary format. Serialization is often used for tasks like saving object state, sending data over a network, or storing data in a persistent storage system. In Python, the term "serialization" is commonly associated with two modules: `pickle` and `json`.

    25. Python lambda function: 

    26. n Python, a lambda function is a small, anonymous function defined using the `lambda` keyword. Lambda functions are often used for short, simple operations where a full function definition using `def` would be more cumbersome. The syntax for a lambda function is:

        ```
        pythonCopy code
        lambda arguments: expression
        ```

        Here's a simple example:

        ```
        pythonCopy code
        # Regular function
        def square(x):
            return x ** 2
        
        print(square(5))  # Output: 25
        
        # Equivalent lambda function
        square_lambda = lambda x: x ** 2
        
        print(square_lambda(5))  # Output: 25
        ```

        In this example, the lambda function `lambda x: x ** 2` is equivalent to the regular function `square(x)`.

        Lambda functions are often used in situations where a small function is needed for a short period, and a full function definition would be overkill. They are commonly used in functions like `map()`, `filter()`, and `sorted()`. Here are a few more examples:

        ```
        pythonCopy code
        # Using lambda with map()
        numbers = [1, 2, 3, 4, 5]
        squared_numbers = list(map(lambda x: x ** 2, numbers))
        print(squared_numbers)  # Output: [1, 4, 9, 16, 25]
        
        # Using lambda with filter()
        even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
        print(even_numbers)  # Output: [2, 4]
        
        # Using lambda with sorted()
        sorted_numbers = sorted(numbers, key=lambda x: x % 3)
        print(sorted_numbers)  # Output: [3, 1, 4, 2, 5]
        ```

        These examples demonstrate the use of lambda functions in combination with built-in functions for concise and expressive code. Keep in mind that lambda functions are limited in complexity and are best suited for simple, one-line expressions.

        26. f"{}"

            In Python, an f-string is a formatted string literal that allows you to embed expressions inside string literals, using curly braces `{}`. These expressions are evaluated at runtime and formatted using the surrounding string. Here's an example:

            ```
            pythonCopy code
            variable = 42
            formatted_string = f'The value of the variable is {variable}'
            print(formatted_string)
            ```

            In this case, `{variable}` is an expression inside the f-string, and it will be replaced with the value of the variable at runtime.

            Now, if you have the f-string `f'a'`, it's a simple string literal because there are no expressions or variables inside the curly braces. It's equivalent to the regular string `'a'`. The f-string feature is not being utilized in this case.

            ```
            pythonCopy code
            simple_f_string = f'a'
            print(simple_f_string)  # Output: 'a'
            ```

            If there are no expressions or variables to be evaluated within the curly braces, you can simply use a regular string instead of an f-string.

        27. a = [1,2,3] a is an iterable but not . map(f, list) filter() return an iterable and join() can be applied on an iterable.

        28. map(func, iterable) return an iterable, func here should be the function name for example str or a lambda

        29. stack is just a list, append as push, pop as pop, pop always pop the last element, if empty raises IndexError, so need to make sure stack is not empty before pop

        30. Python customized sort:
            If you want to sort the list of `Student` objects in non-increasing order (descending order) based on a specific attribute, you can modify the key function accordingly. You can use the `reverse` parameter of the `sorted()` function to indicate that you want the sorting in descending order.

            Here's an example sorting the `Student` objects in non-increasing order based on the `student_id` attribute:

            ```
            pythonCopy code
            class Student:
                def __init__(self, student_id, name):
                    self.student_id = student_id
                    self.name = name
            
            # Create a list of Student objects
            students = [
                Student(3, 'Alice'),
                Student(1, 'Bob'),
                Student(2, 'Charlie')
            ]
            
            # Define a custom sorting function based on the student_id attribute
            def custom_sort(student):
                return student.student_id
            
            # Use the sorted() function with the custom sorting function and reverse=True
            sorted_students = sorted(students, key=custom_sort, reverse=True)
            
            # Print the sorted list of Student objects
            for student in sorted_students:
                print(f"ID: {student.student_id}, Name: {student.name}")
            ```

            In this example, setting `reverse=True` in the `sorted()` function sorts the list in descending order based on the `student_id` attribute.

            You can also use a lambda function with `reverse=True` for a more concise approach:

            ```
            pythonCopy code
            sorted_students = sorted(students, key=lambda x: x.student_id, reverse=True)
            ```

            Adjust the key function and the `reverse` parameter based on your specific requirements.

            31. In the context of mathematical operations and programming, "truncate" refers to the process of discarding the fractional part of a number, essentially rounding towards zero. Truncation always moves towards zero regardless of the sign of the number.

                For example:

                - Truncating 3.9 results in 3.
                - Truncating -2.7 results in -2.
                - Truncating 0.001 results in 0.

                In Python, the `math.trunc()` function is specifically designed to truncate a floating-point number, returning the integer part without rounding. Keep in mind that truncation simply removes the decimal part without considering rounding rules; it always moves towards zero.

                python // round toward -inf, c++ and java / round towards 0

            32. judge if is char and if is a number

                ```python
                a = 'é'
                b = 'A'
                a.isalpha() and a.isascii() # False
                b.isapha() and b.isascii() # True
                c = '1'
                c.isdigit() # True
                ```

            33. In Python, the equivalent of C++'s `lower_bound` and `upper_bound` functions can be achieved using the `bisect` module. The `bisect` module provides functions to perform binary searches on sorted sequences. Specifically, you can use `bisect_left` for `lower_bound` and `bisect_right` for `upper_bound`.

                Here's an example:

                ```python
                pythonCopy code
                from bisect import bisect_left, bisect_right
                
                def lower_bound(arr, target):
                    return bisect_left(arr, target)
                
                def upper_bound(arr, target):
                    return bisect_right(arr, target)
                
                # Example usage:
                sorted_array = [1, 2, 2, 4, 4, 4, 7, 8, 9, 10]
                
                target_element = 4
                
                lower_bound_index = lower_bound(sorted_array, target_element)
                upper_bound_index = upper_bound(sorted_array, target_element)
                
                print(f"Lower bound of {target_element}: {lower_bound_index}")
                print(f"Upper bound of {target_element}: {upper_bound_index}")
                ```

                In this example, `lower_bound` returns the index of the first element greater than or equal to the target, and `upper_bound` returns the index of the first element strictly greater than the target.

                Make sure the array is sorted before using these functions. If the array is not sorted, the results may not be accurate. The `bisect` module is part of the Python standard library, so you don't need to install any additional packages to use it.

            34. In Python, function arguments with default values must be specified after arguments without default values. The order is important, and you should define parameters with default values after those without default values.

            35. python deque:

            36. 
                In Python, a `deque` (double-ended queue) is a versatile data structure that allows you to add and remove elements from both ends with O(1) time complexity. It is implemented in the `collections` module. To use a deque, you need to import it:

                ```
                pythonCopy code
                from collections import deque
                ```

                Here are some common operations and methods associated with `deque`:

                1. **Creating a Deque:**

                   ```
                   pythonCopy code
                   my_deque = deque()
                   ```

                2. **Appending and Popping Elements:**

                   ```
                   pythonCopy code
                   my_deque.append(1)    # Append to the right
                   my_deque.appendleft(2)  # Append to the left
                   element = my_deque.pop()       # Remove and return the rightmost element
                   leftmost_element = my_deque.popleft()  # Remove and return the leftmost element
                   ```

                3. **Accessing Elements:**

                   ```
                   pythonCopy code
                   first_element = my_deque[0]
                   last_element = my_deque[-1]
                   ```

                4. **Checking if Deque is Empty:**

                   ```
                   pythonCopy code
                   is_empty = not my_deque  # True if empty, False if not
                   ```

                5. **Length of Deque:**

                   ```
                   pythonCopy code
                   length = len(my_deque)
                   ```

                6. **Clearing the Deque:**

                   ```
                   pythonCopy code
                   my_deque.clear()
                   ```

                7. **Rotating the Deque:**

                   ```
                   pythonCopy code
                   my_deque.rotate(1)  # Rotate one step to the right (use -1 for left)
                   ```

                8. **Converting List to Deque:**

                   ```
                   pythonCopy code
                   my_list = [1, 2, 3]
                   my_deque = deque(my_list)
                   ```

                9. **Appending Multiple Elements:**

                   ```
                   pythonCopy code
                   my_deque.extend([4, 5, 6])      # Extend to the right
                   my_deque.extendleft([3, 2, 1])  # Extend to the left
                   ```

                10. **Removing a Specific Element:**

                    ```
                    pythonCopy code
                    my_deque.remove(2)  # Remove the first occurrence of the specified element
                    ```

                11. **Counting Occurrences:**

                    ```
                    pythonCopy code
                    count_of_1 = my_deque.count(1)
                    ```

                `deque` is particularly useful when you need a fast queue or stack implementation, or when you frequently need to add or remove elements from both ends of a collection. The `collections` module provides an efficient implementation of the deque data structure that outperforms list-based approaches in certain scenarios.

            37. python dict:

            38. In Python, dictionaries are versatile data structures that allow you to store and retrieve key-value pairs efficiently. Here are some commonly used methods associated with Python dictionaries:

                1. **Creating a Dictionary:**

                   ```
                   pythonCopy code
                   my_dict = {}  # or my_dict = dict()
                   ```

                2. **Adding or Updating Key-Value Pairs:**

                   ```
                   pythonCopy code
                   my_dict['key1'] = 'value1'
                   my_dict.update({'key2': 'value2', 'key3': 'value3'})
                   ```

                3. **Accessing Values:**

                   ```
                   pythonCopy code
                   value = my_dict['key1']
                   ```

                4. **Getting Values with a Default:**

                   ```
                   pythonCopy code
                   value = my_dict.get('key1', 'default_value')
                   ```

                5. **Checking if a Key Exists:**

                   ```
                   pythonCopy code
                   if 'key1' in my_dict:
                       # Key exists
                   ```

                6. **Removing a Key-Value Pair:**

                   ```
                   pythonCopy code
                   del my_dict['key1']
                   value = my_dict.pop('key2')  # Removes and returns the value
                   ```

                7. **Iterating Over Keys, Values, or Items:**

                   ```
                   pythonCopy code
                   for key in my_dict:
                       print(key)
                   
                   for value in my_dict.values():
                       print(value)
                   
                   for key, value in my_dict.items():
                       print(key, value)
                   ```

                8. **Dictionary Comprehension:**

                   ```
                   pythonCopy code
                   squared_dict = {key: key**2 for key in range(5)}
                   ```

                9. **Clearing a Dictionary:**

                   ```
                   pythonCopy code
                   my_dict.clear()
                   ```

                10. **Copying a Dictionary:**

                    ```
                    pythonCopy code
                    new_dict = my_dict.copy() # shallow copy
                    ```

                11. **Merging Dictionaries (Python 3.9 and later):**

                    ```
                    pythonCopy code
                    merged_dict = {**dict1, **dict2}
                    ```

                12. **Dictionary Length:**

                    ```
                    pythonCopy code
                    length = len(my_dict)
                    ```

                13. **Sorting a Dictionary by Key:**

                    ```
                    pythonCopy code
                    sorted_dict = dict(sorted(my_dict.items()))
                    ```

                14. **Sorting a Dictionary by Value:**

                    ```
                    pythonCopy code
                    sorted_dict = dict(sorted(my_dict.items(), key=lambda item: item[1]))
                    ```

                These are just some of the many methods and operations you can perform on Python dictionaries. Depending on your specific use case, you may find other methods that suit your needs.

            39. Python OrderedDict:

            40. `OrderedDict` is a dictionary subclass in Python that maintains the order in which items were inserted. It is part of the `collections` module. Here are some common methods and operations associated with `OrderedDict`:

                1. **Creating an OrderedDict:**

                   ```
                   pythonCopy code
                   from collections import OrderedDict
                   
                   my_ordered_dict = OrderedDict()
                   ```

                2. **Adding or Updating Key-Value Pairs:**

                   ```
                   pythonCopy code
                   my_ordered_dict['a'] = 1
                   my_ordered_dict.update({'b': 2, 'c': 3})
                   ```

                3. **Accessing Values:**

                   ```
                   pythonCopy code
                   value = my_ordered_dict['a']
                   ```

                4. **Iterating Over Items (Maintains Insertion Order):**

                   ```
                   pythonCopy code
                   for key, value in my_ordered_dict.items():
                       print(key, value)
                   ```

                5. **Moving an Element to the End:**

                   ```
                   pythonCopy code
                   my_ordered_dict.move_to_end('a')
                   ```

                6. **Checking if a Key Exists:**

                   ```
                   pythonCopy code
                   if 'a' in my_ordered_dict:
                       # Key exists
                   ```

                7. **Removing a Key-Value Pair:**

                   ```
                   pythonCopy code
                   del my_ordered_dict['a']
                   value = my_ordered_dict.pop('b')  # Removes and returns the value
                   ```

                8. **Popitem (Remove and Return Last Inserted Pair):**

                   ```
                   pythonCopy code
                   key, value = my_ordered_dict.popitem()
                   ```

                9. **Reversing the Order:**

                   ```
                   pythonCopy code
                   reversed_dict = OrderedDict(reversed(my_ordered_dict.items()))
                   ```

                10. **Clearing the OrderedDict:**

                    ```
                    pythonCopy code
                    my_ordered_dict.clear()
                    ```

                11. **Copying an OrderedDict:**

                    ```
                    pythonCopy code
                    new_ordered_dict = my_ordered_dict.copy()
                    ```

                12. **Merging OrderedDictionaries:**

                    ```
                    pythonCopy code
                    merged_ordered_dict = OrderedDict(my_ordered_dict1, **my_ordered_dict2)
                    ```

                13. **Equality Check:**

                    ```
                    pythonCopy code
                    are_equal = my_ordered_dict1 == my_ordered_dict2
                    ```

                14. **Dictionary Length:**

                    ```
                    pythonCopy code
                    length = len(my_ordered_dict)
                    ```

                15. **Setting Default Values:**

                    ```
                    pythonCopy code
                    my_ordered_dict.setdefault('a', 0)  # If 'a' is not present, set it to 0
                    ```

                `OrderedDict` is particularly useful when the order of insertion of key-value pairs is important, and you need to maintain that order throughout the lifetime of the dictionary.

            41. Not in standard library cannot directly use!! (Possible equivalence to c++ set(tree))In Python, the `set` data structure is implemented using a hash table, not a tree. However, if you're looking for a data structure in Python that is similar to a C++ `std::set` and implemented as a tree, you can use the `sortedcontainers` library, specifically the `SortedSet` class.

                Here's an example:

                ```
                pythonCopy code
                from sortedcontainers import SortedSet
                
                # Create a SortedSet
                my_set = SortedSet([3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5])
                
                # Operations similar to a set
                my_set.add(8)
                my_set.remove(4)
                print(my_set)
                
                # Iterating over the set in sorted order
                for item in my_set:
                    print(item)
                ```

                In this example, the `SortedSet` from the `sortedcontainers` library behaves like a set and maintains its elements in sorted order, which is achieved through a tree-based data structure. The library uses a self-balancing binary search tree (specifically, a red-black tree) under the hood to maintain the sorted order of elements.

                You can install the `sortedcontainers` library using:

                ```
                bashCopy code
                pip install sortedcontainers
                ```

                Keep in mind that Python's built-in `set` is optimized for general use cases and provides fast average-case time complexity for common set operations. If you don't specifically need a tree-based set, the built-in `set` is usually a more convenient and performant choice.

            42. Python slicing such as arr[0:1] will create a new object instead modify to the original array

            43. python sorted(dict) will return a list of keys in order, and dict and OrderedDict or defaultdict are all preserve the order the key is created and inserted into dict, update won't change the order.

            44. Pay special attention: python set and deque should be init on list,

                ```python
                s = set("ab") # ['a', 'b']
                s = set(["ab"]) # ["ab"]
                q = deque([(1,1)]) # [(1,1)]
                q = deque((1,1)) # error since the thing should be iterable
                ```

            45. python nonlocal and global:

                nonlocal: The `nonlocal` keyword is used to work with variables inside nested functions, where the variable should not belong to the inner function. ( And you want to modify that variable inside nested functions, if not nonlocal added, a new var will be created and not refers to the outside variable)

                but when not modifying just use as an right val to need to include that keyword

                Use the keyword `nonlocal` to declare that the variable is not local.

                global: The `global` keyword is used to create global variables from a no-global scope, e.g. inside a function.

            46. range(len(q)) can be used to level-order trasversal for tree because range is determined and constructed the first cycle and thus won't changed in the middle of the for loop.
            
            47. python float and int can compare and result depend on real larger or smaller, 2.00 == 2 returns True, so we can use float('inf') and float('-inf') for infinity need
            
            48. fill a array with 0 in place: a[:] = [0] * len(a)
            
            49. python find a index of a val in a list: idx = arr.index(val, start(optional), end(optional)) and if not found raise valueError, that would be faster than a self-written for loop becuase the built-in func is implemented in c and optimized for performance
            
            50. all things in python is pass by reference, but just immutable object such as integer or string or tuple cannot be modified in-place, any assignment cause the creation of a new object, so it seems like pass by value but not.
            
            51. python max() and min() can take multiple arguments (more than two)
            
            52. << and >> is of very low priority, even lower than + -, so 1 + 1 << d is not equal to 1 + (1<<d) but 0 << d
            
            53. python mutable object has method .copy() that create a shallow copy of itself, immutable object like int, string do not have that method. For string:
                ```python
                a = "1"
                b = a
                print(id(a) == id(b)) # return True
                ```
            
                mutable .copy():
            
                ```python
                a = [1]
                b = a.copy()
                print(id(a) == id(b)) # return False since b will create a new object but it is a shallow copy that inner element are just reference to the original object's inner elements, 
                print(id(a[0]) == id(b[0])) # return True
                a[0] = 2
                print(id(a[0]) == id(b[0])) # return False since int is immutable, changes to it are just create a new object, if elements inside are mutable such as lists, then modify it will also reflected in its shallow copies.
                ```
            
                if really want deep copy:
            
                ```python
                import copy.deepcopy
                a = [1]
                b = deepcopy(a)
                print(id(a[0]) == id(b[0])) # Still True because https://stackoverflow.com/questions/31621997/why-deepcopy-of-list-of-integers-returns-the-same-integers-in-memory
                # but for non-atomic it will return False
                a = [[1,2]]
                b = deepcopy(a)
                c = a.copy()
                print(id(a[0]) == id(b[0])) # False
                print(id(c[0]) == id(a[0])) # True
                ```
            
                deepcopy is to defend against mutability for nested structure inner element, if inner is immutable then no need to defend thus immutable itself is returned.
            
            54. Python str.count(c, start(optional), end(optional)):
            
                In Python, the `str.count()` method is used to count the occurrences of a substring within a given string. The method takes a substring as an argument and returns the number of non-overlapping occurrences of that substring in the original string.
            
                Here's the basic syntax:
            
                ```python
                pythonCopy code
                str.count(substring, start, end)
                ```
            
                - `substring`: The substring you want to count in the original string.
                - `start` (optional): The starting index for the search (default is 0).
                - `end` (optional): The ending index for the search (default is the end of the string).
            
                Here's an example:
            
                ```python
                pythonCopy code
                sentence = "This is a sample sentence. This sentence is just an example."
                
                # Count the occurrences of the substring "sentence"
                count = sentence.count("sentence")
                
                print("Number of occurrences:", count)
                ```
            
                In this example, the output would be:
            
                ```python
                javascriptCopy code
                Number of occurrences: 2
                ```
            
                The `count` method is case-sensitive, so it distinguishes between uppercase and lowercase characters. If you want to perform a case-insensitive count, you can convert both the original string and the substring to lowercase (or uppercase) using the `lower()` or `upper()` method:
            
                ```python
                pythonCopy code
                sentence = "This is a sample sentence. This sentence is just an example."
                
                # Count the occurrences of the substring "sentence" in a case-insensitive manner
                count = sentence.lower().count("sentence".lower())
                
                print("Number of occurrences:", count)
                ```
            
                This would also output:
            
                ```python
                javascriptCopy code
                Number of occurrences: 2
                ```

24. According to the [heapq documentation](http://docs.python.org/library/heapq.html), the way to customize the heap order is to have each element on the heap to be a tuple, with the first tuple element being one that accepts normal Python comparisons.
25. python heapify is O(nlogn) but more strictly it is linear time O(n), see here for the math: https://python.plainenglish.io/heapify-in-linear-time-114a15487ba1
26. python dict key must be immutable: **If the key were a mutable object, its value could change, and thus its hash could also change**, we cannot let that happens.
27. a important matter of fact for [obj] * n

    ```python
    a = [1] * 5
    a[0] = 6
    print(a)
    # [6, 1, 1, 1, 1]
    # [obj] * n is create n reference to one object obj in a list.
    # int is immutable, so modify the value is actually create a new int object located at another address other than the original address of 1
    
    b = [{}] * 5
    b[0][0] = 0
    print(b)
    # [{0: 0}, {0: 0}, {0: 0}, {0: 0}, {0: 0}]
    
    c = [{} for _ in range(5)]
    c[0][0] = 0 
    print(c)
    # [{0: 0}, {}, {}, {}, {}]
    ```

    