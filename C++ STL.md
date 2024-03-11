# C++ STL

## std::find_if

```c++
template<class InputIterator, class UnaryPredicate>
  InputIterator find_if (InputIterator first, InputIterator last, UnaryPredicate pred)
{
  while (first!=last) {
    if (pred(*first)) return first;
    ++first;
  }
  return last;
}
```

Very useful when find an element in a std::list.

## std::list



## std::accumulate

```c++
template <class InputIterator, class T>
   T accumulate (InputIterator first, InputIterator last, T init)
{
  while (first!=last) {
    init = init + *first;  // or: init=binary_op(init,*first) for the binary_op version
    ++first;
  }
  return init;
}
```

We can use & in [&] for lambda to indicate that the lambda function can access (read and modify) all variables from the surrounding scope by reference.

## std::fill

```c++
template<class ForwardIt, class T>
void fill(ForwardIt first, ForwardIt last, const T& value)
{
    for (; first != last; ++first)
        *first = value;
}
```

## std::sort

**Q:** what is the default behavior for that if I do not use customized comparator?

**A:** If you do not provide a custom comparator when sorting a vector of vectors using `std::sort`, the default behavior will be to sort the vector of vectors based on the lexicographical (dictionary) order of the inner vectors.

In other words, the sorting will consider the elements of the inner vectors from left to right, comparing the first elements of the vectors first, and if they are equal, it will move on to compare the second elements, and so on. This is known as lexicographical ordering.

## std::vector

To return a vector, one can just do:
```c++
return {1, 2, 3};
```

Can use this to create a vector of empty vector
```c++
vector<vector<int>> adjList(n, vector<int>{});
```

## std::unique

Removes all but the first element from every consecutive group of equivalent elements in the range `[first,last)`.

return a iterator to past-the-end of the new logical end of the range (which is now unique).

So we need to do resize or erase to make sure the new end to the old end is eliminated (right now is indeterminate), but not always necessary to do so.

```c++
template <class ForwardIterator>
  ForwardIterator unique (ForwardIterator first, ForwardIterator last)
{
  if (first==last) return last;

  ForwardIterator result = first;
  while (++first != last)
  {
    if (!(*result == *first))  // or: if (!pred(*result,*first)) for version (2)
      *(++result)=*first;
  }
  return ++result;
}
```



## std::memset

```c++
void * memset ( void * ptr, int value, size_t num ); // num is the actually bytes of the memory to be allocated.
```

```
vector<int> a[100];
memset(a, 100, sizeof a);
```

## std::tuple

```c++
tuple<int, int, char, int> a = make_tuple(1, 1, 'a', 1);
cout << get<0>(a) << endl;
cout << get<3>(a) << endl;
```

## std::deque

emplace_back() , pop_front() pop_back() emplace_front() front() back() 

iterator: begin() end()
